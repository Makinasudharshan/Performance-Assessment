🧪 HTTPBin Post API Performance Test Suite (JMeter + Docker Compose)
📌 Overview

This project provides a complete performance testing setup using Apache JMeter and Docker Compose to benchmark the following HTTP methods of httpbin:

GET → /get

POST → /post

PUT → /put

DELETE → /delete

PATCH → /patch

The suite helps validate performance KPIs like response time, throughput, and error rates under different load conditions.

⚙️ Project Structure
├── docker-compose.yml
├── httpbin_api_test.jmx          # JMeter Test Plan
├── results/                      # Raw JTL results
├── report-html/                  # Generated HTML reports
└── README.md                     # Documentation

🚀 Setup Instructions
1️⃣ Run via Docker Compose (Recommended)
docker-compose up


Spins up the HTTPBin service at http://localhost:8000

Executes the JMeter test in non-GUI mode

Generates HTML performance reports automatically

📄 Reports generated at:

Raw results: results/results.jtl

HTML dashboard: report-html/index.html

2️⃣ Run JMeter GUI (Optional)

For exploratory testing or modifying scenarios:

jmeter


Open PostBin_Test.jmx in JMeter GUI

Adjust Thread Group for user count, ramp-up, and duration

Run the test and analyze results with listeners

🧰 Tools Used

🧪 Apache JMeter – Open-source performance testing tool


📝 Performance Testing Approach
📍 1. Requirement Analysis

Reviewed NFRs (Non-Functional Requirements): expected user load, peak load, SLAs, and system architecture.

Identified key business transactions .

📊 2. Workload Modeling

Defined concurrent user count, test duration, and ramp-up/down based on real or projected traffic.

Distributed user load across endpoints to mimic real usage patterns.

🧪 3. Test Scenario Design
Test Type	Objective	Example Config
Load Test	Validate performance under expected load	100 users for 15 min
Stress Test	Identify system breaking point	Gradual ramp-up beyond expected traffic
Endurance (Soak) Test	Check stability & memory leaks over time	100 users for 2 hrs
Spike Test	Assess resilience to sudden traffic spikes	0 → 1200 users instantly, then back down
🧭 Execution via CLI (Alternative)
nohup ./jmeter -n \
  -t PostBin_Test.jmx \
  -l results/soaktest.jtl \
  -e -o report-html/soaktest \
  > results/soaktest.log 2>&1 &


✅ Keeps the test running in the background (nohup)
📈 Logs stored in results/soaktest.log
📊 Dashboard report at report-html/soaktest/index.html

📡 Monitoring & Analysis

JMeter HTML Dashboard – Key metrics (response time, throughput, error %).

Monitor resource utilization (CPU, Memory, Network) on server/container.

Capture any failures or errors in the JTL logs for RCA.

🏁 Next Steps

Integrate with CI/CD (e.g., Jenkins) for automated performance runs.

Add custom assertions & SLAs in the JMeter test plan.
