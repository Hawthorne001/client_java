# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-03-31T13:47:53Z
- **Commit:** [`6beb7fd`](https://github.com/Hawthorne001/client_java/commit/6beb7fd3f26fb1629aae21d9d85d975f63d1a6b8)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1008-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.32K | ± 1.34K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.77K | ± 443.30 | ops/s | 1.2x slower |
| prometheusAdd | 51.19K | ± 376.71 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 50.26K | ± 864.21 | ops/s | 1.3x slower |
| simpleclientInc | 6.58K | ± 178.32 | ops/s | 9.9x slower |
| simpleclientNoLabelsInc | 6.38K | ± 196.08 | ops/s | 10x slower |
| simpleclientAdd | 6.01K | ± 167.84 | ops/s | 11x slower |
| openTelemetryAdd | 1.67K | ± 381.39 | ops/s | 39x slower |
| openTelemetryIncNoLabels | 1.35K | ± 224.45 | ops/s | 48x slower |
| openTelemetryInc | 1.27K | ± 71.77 | ops/s | 51x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.90K | ± 898.07 | ops/s | **fastest** |
| simpleclient | 4.49K | ± 58.38 | ops/s | 1.3x slower |
| prometheusNative | 2.98K | ± 282.83 | ops/s | 2.0x slower |
| openTelemetryClassic | 720.28 | ± 45.64 | ops/s | 8.2x slower |
| openTelemetryExponential | 561.20 | ± 7.44 | ops/s | 11x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 476.70K | ± 1.83K | ops/s | **fastest** |
| prometheusWriteToByteArray | 473.19K | ± 5.70K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 460.51K | ± 6.13K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 457.10K | ± 6.54K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      50256.288    ± 864.211  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1670.839    ± 381.392  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1271.734     ± 71.766  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1350.004    ± 224.455  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51189.848    ± 376.706  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65315.845   ± 1344.564  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56767.015    ± 443.300  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6006.477    ± 167.839  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6581.039    ± 178.316  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6376.413    ± 196.083  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        720.279     ± 45.638  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        561.205      ± 7.438  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5903.846    ± 898.070  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2977.051    ± 282.828  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4487.766     ± 58.382  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     457097.195   ± 6542.691  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     460506.817   ± 6134.980  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     473187.299   ± 5703.845  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     476699.087   ± 1830.849  ops/s
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
