# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-03-16T07:59:03Z
- **Commit:** [`b81332e`](https://github.com/Hawthorne001/client_java/commit/b81332e3a09e465f956f118a2403e64b83771ae5)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.14.0-1017-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.61K | ± 1.58K | ops/s | **fastest** |
| prometheusNoLabelsInc | 57.04K | ± 519.48 | ops/s | 1.2x slower |
| prometheusAdd | 51.61K | ± 204.69 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 49.24K | ± 1.52K | ops/s | 1.3x slower |
| simpleclientNoLabelsInc | 6.63K | ± 119.72 | ops/s | 9.9x slower |
| simpleclientInc | 6.58K | ± 36.48 | ops/s | 10.0x slower |
| simpleclientAdd | 6.27K | ± 218.82 | ops/s | 10x slower |
| openTelemetryInc | 1.37K | ± 248.35 | ops/s | 48x slower |
| openTelemetryIncNoLabels | 1.35K | ± 224.08 | ops/s | 49x slower |
| openTelemetryAdd | 1.26K | ± 28.93 | ops/s | 52x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 6.02K | ± 1.35K | ops/s | **fastest** |
| simpleclient | 4.58K | ± 22.27 | ops/s | 1.3x slower |
| prometheusNative | 2.82K | ± 439.07 | ops/s | 2.1x slower |
| openTelemetryClassic | 704.72 | ± 35.76 | ops/s | 8.5x slower |
| openTelemetryExponential | 586.77 | ± 26.03 | ops/s | 10x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 495.57K | ± 1.52K | ops/s | **fastest** |
| prometheusWriteToByteArray | 490.02K | ± 1.83K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 476.99K | ± 5.56K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 473.37K | ± 8.00K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49235.460   ± 1521.471  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1262.120     ± 28.927  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1373.817    ± 248.352  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1346.033    ± 224.081  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51608.221    ± 204.694  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65613.922   ± 1580.171  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      57041.929    ± 519.478  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6267.113    ± 218.822  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6578.757     ± 36.480  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6626.404    ± 119.723  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        704.723     ± 35.764  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        586.768     ± 26.030  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6024.697   ± 1346.855  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2820.734    ± 439.073  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4575.314     ± 22.274  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     473370.401   ± 7998.451  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     476988.051   ± 5557.430  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     490020.865   ± 1830.698  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     495570.835   ± 1523.007  ops/s
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
