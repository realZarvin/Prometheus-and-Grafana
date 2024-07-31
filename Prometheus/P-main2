use actix_web::{web, App, HttpServer, Responder};
use prometheus::{Encoder, TextEncoder, IntCounter, register_int_counter};
use std::sync::Arc;
use tokio::sync::Mutex;

struct AppState {
    counter: IntCounter,
}

async fn metrics(data: web::Data<Arc<Mutex<AppState>>>) -> impl Responder {
    let encoder = TextEncoder::new();
    let mut buffer = Vec::new();

    let state = data.lock().await;
    let metric_families = prometheus::gather();
    encoder.encode(&metric_families, &mut buffer).unwrap();

    drop(state);
    String::from_utf8(buffer).unwrap()
}

async fn index(data: web::Data<Arc<Mutex<AppState>>>) -> impl Responder {
    let state = data.lock().await;
    state.counter.inc();
    drop(state);
    "Hello, world!"
}

#[actix_web::main]
async fn main() -> std::io::Result<()> {
    let counter = register_int_counter!("requests_total", "Total number of requests").unwrap();
    let app_state = Arc::new(Mutex::new(AppState { counter }));

    HttpServer::new(move || {
        App::new()
            .app_data(web::Data::new(app_state.clone()))
            .route("/", web::get().to(index))
            .route("/metrics", web::get().to(metrics))
    })
    .bind("0.0.0.0:8000")?
    .run()
    .await
}
