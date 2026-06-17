# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-06-16T07:57:58Z
- **Commit:** [`9672749`](https://github.com/Hawthorne001/client_java/commit/9672749085f9029ccb7328b3e88e8e78fa29e402)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.11K | ± 1.24K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.99K | ± 406.70 | ops/s | 1.1x slower |
| prometheusAdd | 51.30K | ± 371.38 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 47.83K | ± 753.47 | ops/s | 1.4x slower |
| simpleclientInc | 6.60K | ± 90.79 | ops/s | 9.9x slower |
| simpleclientAdd | 6.47K | ± 14.47 | ops/s | 10x slower |
| simpleclientNoLabelsInc | 6.37K | ± 30.82 | ops/s | 10x slower |
| openTelemetryAdd | 3.41K | ± 375.88 | ops/s | 19x slower |
| openTelemetryInc | 3.37K | ± 247.85 | ops/s | 19x slower |
| openTelemetryIncNoLabels | 3.12K | ± 255.89 | ops/s | 21x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.42K | ± 1.57K | ops/s | **fastest** |
| simpleclient | 4.33K | ± 112.65 | ops/s | 1.3x slower |
| prometheusNative | 3.05K | ± 205.77 | ops/s | 1.8x slower |
| openTelemetryClassic | 746.72 | ± 29.85 | ops/s | 7.3x slower |
| openTelemetryExponential | 625.36 | ± 97.39 | ops/s | 8.7x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| openMetricsWriteToNull | 23.57K | ± 300.44 | ops/s | **fastest** |
| prometheusWriteToNull | 23.51K | ± 493.64 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 507.92K | ± 6.23K | ops/s | **fastest** |
| prometheusWriteToByteArray | 494.49K | ± 7.88K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 485.83K | ± 6.10K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 478.81K | ± 5.30K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      47832.096    ± 753.465  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       3413.226    ± 375.882  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       3373.594    ± 247.853  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       3123.458    ± 255.890  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51298.575    ± 371.378  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65108.670   ± 1239.042  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56994.846    ± 406.700  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6465.932     ± 14.475  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6598.535     ± 90.786  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6365.302     ± 30.822  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        746.718     ± 29.850  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        625.355     ± 97.385  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5421.122   ± 1566.824  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3050.471    ± 205.767  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4326.975    ± 112.650  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      23566.615    ± 300.439  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      23511.475    ± 493.637  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     478814.377   ± 5297.602  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     485828.035   ± 6095.861  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     494492.965   ± 7875.886  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     507921.323   ± 6233.363  ops/s
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
