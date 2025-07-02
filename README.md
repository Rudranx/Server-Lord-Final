
````markdown
# 🛡️ Server Lord — Scalable Cron Job Monitoring System

![Go Version](https://img.shields.io/badge/go-1.18+-blue.svg)
![PostgreSQL](https://img.shields.io/badge/database-PostgreSQL-blue)
![OpenTelemetry](https://img.shields.io/badge/observability-OpenTelemetry-ff69b4)
![License](https://img.shields.io/badge/license-MIT-green.svg)

**Server Lord** is a high-performance, scalable cron job monitoring platform built to provide **real-time tracking**, **failure alerts**, and **performance visibility** across thousands of background tasks and users. Inspired by platforms like [Dead Man’s Snitch](https://deadmanssnitch.com) and [Healthchecks.io](http://healthchecks.io), it enables developers and system admins to eliminate silent failures in scheduled scripts or jobs.

> ⚙ Built with **Golang**, **PostgreSQL (with sharding)**, and **OpenTelemetry**  
> 🧠 Handles up to **100,000 tasks** with monitoring latency under **250ms**

---

## 🚀 Features

- ✅ **Multi-user cron monitoring**
- ⏱️ Real-time heartbeat tracking
- ⚠️ Push-based failure alerts
- 📊 Built-in observability via OpenTelemetry
- 🌐 Horizontal scalability with PostgreSQL sharding
- 🧵 Concurrency-safe via goroutines + semaphores

---

## 🏗️ System Architecture

1. **Task creation scripts** generate heartbeat schedules for each user.
2. Cron jobs send periodic heartbeats to the server.
3. Server monitors the tasks via sharded workers (one per shard).
4. Failures or missed heartbeats are logged and flagged for action.
5. Metrics are captured using **OpenTelemetry** for real-time analysis.

---

## 🧰 Tech Stack

| Layer        | Technology                 |
|--------------|-----------------------------|
| Backend      | Golang (Goroutines, Fiber) |
| Database     | PostgreSQL with sharding   |
| Monitoring   | OpenTelemetry              |
| Frontend     | Next.js (if included)      |
| Architecture | Semaphore-based concurrency |

---

## 📦 Installation & Setup

### 1️⃣ Clone the repo
```bash
git clone git@github.com:Rudranx/Server-Lord-Final.git
cd Server-Lord-Final
````

### 2️⃣ Install dependencies

Ensure you have Go installed (v1.18+), then:

```bash
go mod tidy
```

Also, install PostgreSQL and ensure sharding is enabled (e.g., via [Citus](https://www.citusdata.com/)).

### 3️⃣ Configure environment

Set up your environment variables:

```env
DB_HOST=localhost
DB_PORT=5432
DB_USER=your_user
DB_PASS=your_password
DB_NAME=serverlord_db
SHARD_COUNT=4
```

> You can also use `.env` and a parser library like `godotenv`.

### 4️⃣ Run the server

```bash
go run main.go
```

---

## 🧪 Stress Test Results

* 10,000 users and 100,000 cron jobs
* Sub-250ms monitoring latency across shards
* Pull → Push model shift reduced DB polling load drastically

---

## 📈 Observability with OpenTelemetry

To visualize system performance:

1. Run a telemetry collector like **Prometheus or Grafana**
2. Integrate OpenTelemetry client in `main.go`
3. Watch live metrics on dashboards

---

## 🧠 Challenges Faced

* Race conditions during concurrent heartbeat processing
* Query slowdowns due to growing task volume
* Lack of observability in early phases

✅ Solved via:

* Semaphore-based concurrency
* PostgreSQL sharding
* Push-based task tracking
* Full telemetry instrumentation

---

## 🔮 Future Enhancements

* Dynamic configuration scaling based on job traffic
* Priority-based shard scanning
* Cassandra-based alternative backend
* Remote client for bidirectional control & deeper insights

---

## 👨‍💻 Developed By

* Rudransh Kumar Ankodia (`rudransh1896@gmail.com`)

Originally developed with [Adhvaith Hundi](https://github.com/...) and team during **Sanganitra '25**.

---

## 📜 License

MIT License (or add your preferred one)

---

## 📎 References

* [Dead Man’s Snitch](https://deadmanssnitch.com/)
* [Healthchecks.io](http://healthchecks.io/)
* [Golang Concurrency with Context](https://medium.com/@jamal.kaksouri/the-complete-guide-to-context-in-golang-efficient-concurrency-management-43d722f6eaea)
* [OpenTelemetry for Go](https://betterstack.com/community/guides/observability/opentelemetry-metrics-golang/)

````