# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-02-28T20:27:51Z
- **Commit:** [`35735f9`](https://github.com/Hawthorne001/client_java/commit/35735f9e41c5f1eb7dfbf739cc3e3507eeba15a7)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.14.0-1017-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.48K | ± 2.30K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.92K | ± 517.59 | ops/s | 1.2x slower |
| prometheusAdd | 51.48K | ± 397.21 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 49.25K | ± 1.25K | ops/s | 1.3x slower |
| simpleclientInc | 6.66K | ± 113.79 | ops/s | 9.8x slower |
| simpleclientNoLabelsInc | 6.57K | ± 123.51 | ops/s | 10.0x slower |
| simpleclientAdd | 6.35K | ± 288.64 | ops/s | 10x slower |
| openTelemetryAdd | 1.44K | ± 225.59 | ops/s | 45x slower |
| openTelemetryIncNoLabels | 1.37K | ± 195.63 | ops/s | 48x slower |
| openTelemetryInc | 1.32K | ± 186.64 | ops/s | 50x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 6.23K | ± 1.29K | ops/s | **fastest** |
| simpleclient | 4.56K | ± 15.44 | ops/s | 1.4x slower |
| prometheusNative | 2.82K | ± 326.57 | ops/s | 2.2x slower |
| openTelemetryClassic | 680.02 | ± 11.10 | ops/s | 9.2x slower |
| openTelemetryExponential | 556.77 | ± 13.77 | ops/s | 11x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 479.24K | ± 5.58K | ops/s | **fastest** |
| prometheusWriteToByteArray | 471.72K | ± 4.30K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 461.49K | ± 7.32K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 454.88K | ± 7.47K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49245.314   ± 1251.637  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1441.985    ± 225.589  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1320.539    ± 186.645  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1365.954    ± 195.628  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51481.985    ± 397.209  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65476.545   ± 2304.961  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56922.923    ± 517.586  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6346.524    ± 288.641  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6655.877    ± 113.786  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6574.975    ± 123.506  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        680.017     ± 11.103  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        556.765     ± 13.775  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6230.592   ± 1288.640  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2818.369    ± 326.567  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4563.374     ± 15.435  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     454884.225   ± 7471.506  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     461494.567   ± 7323.061  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     471715.792   ± 4297.620  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     479240.255   ± 5579.907  ops/s
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
