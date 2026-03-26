# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-03-26T12:39:30Z
- **Commit:** [`6beb7fd`](https://github.com/Hawthorne001/client_java/commit/6beb7fd3f26fb1629aae21d9d85d975f63d1a6b8)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.14.0-1017-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.33K | ± 1.46K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.98K | ± 311.34 | ops/s | 1.1x slower |
| prometheusAdd | 51.60K | ± 198.05 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 38.56K | ± 12.75K | ops/s | 1.7x slower |
| simpleclientInc | 6.71K | ± 57.30 | ops/s | 9.7x slower |
| simpleclientNoLabelsInc | 6.39K | ± 69.96 | ops/s | 10x slower |
| simpleclientAdd | 6.34K | ± 160.97 | ops/s | 10x slower |
| openTelemetryIncNoLabels | 1.33K | ± 153.49 | ops/s | 49x slower |
| openTelemetryAdd | 1.32K | ± 67.14 | ops/s | 50x slower |
| openTelemetryInc | 1.30K | ± 22.07 | ops/s | 50x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 6.42K | ± 1.31K | ops/s | **fastest** |
| simpleclient | 4.57K | ± 9.43 | ops/s | 1.4x slower |
| prometheusNative | 2.85K | ± 275.53 | ops/s | 2.3x slower |
| openTelemetryClassic | 687.49 | ± 25.67 | ops/s | 9.3x slower |
| openTelemetryExponential | 557.29 | ± 35.26 | ops/s | 12x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToByteArray | 490.99K | ± 3.16K | ops/s | **fastest** |
| prometheusWriteToNull | 490.03K | ± 3.04K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 483.87K | ± 2.37K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 481.21K | ± 3.55K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      38561.713  ± 12745.767  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1315.574     ± 67.138  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1298.072     ± 22.065  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1327.184    ± 153.488  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51601.413    ± 198.052  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65325.328   ± 1461.288  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56983.178    ± 311.340  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6342.178    ± 160.965  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6710.144     ± 57.298  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6385.539     ± 69.956  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        687.490     ± 25.669  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        557.295     ± 35.257  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6424.349   ± 1309.594  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2850.422    ± 275.532  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4574.211      ± 9.432  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     481209.989   ± 3545.441  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     483871.284   ± 2366.233  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     490986.031   ± 3156.018  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     490026.078   ± 3039.818  ops/s
```

## Notes

- **Score** = Throughput in operations per second (higher is better)
- **Error** = 99.9% confidence interval

## Benchmark Descriptions

| Benchmark | Description |
|:----------|:------------|
| **CounterBenchmark** | Counter increment performance: Prometheus, OpenTelemetry, simpleclient, Codahale |
| **HistogramBenchmark** | Histogram observation performance (classic vs native/exponential) |
| **TextFormatUtilBenchmark** | Metric exposition format writing speed |
