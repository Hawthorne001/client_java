# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-04-20T02:00:06Z
- **Commit:** [`4b69f40`](https://github.com/Hawthorne001/client_java/commit/4b69f40bd4e616d69468ce99dc4323162287a577)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** Intel(R) Xeon(R) Platinum 8370C CPU @ 2.80GHz, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1010-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 31.56K | ± 33.77 | ops/s | **fastest** |
| prometheusNoLabelsInc | 31.07K | ± 44.34 | ops/s | 1.0x slower |
| codahaleIncNoLabels | 29.40K | ± 1.36K | ops/s | 1.1x slower |
| prometheusAdd | 26.69K | ± 1.57K | ops/s | 1.2x slower |
| simpleclientInc | 6.95K | ± 157.98 | ops/s | 4.5x slower |
| simpleclientNoLabelsInc | 6.81K | ± 158.83 | ops/s | 4.6x slower |
| simpleclientAdd | 6.55K | ± 179.55 | ops/s | 4.8x slower |
| openTelemetryAdd | 1.39K | ± 88.41 | ops/s | 23x slower |
| openTelemetryInc | 1.37K | ± 140.98 | ops/s | 23x slower |
| openTelemetryIncNoLabels | 1.30K | ± 43.52 | ops/s | 24x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| simpleclient | 4.50K | ± 150.84 | ops/s | **fastest** |
| prometheusClassic | 3.38K | ± 183.96 | ops/s | 1.3x slower |
| prometheusNative | 2.19K | ± 191.44 | ops/s | 2.1x slower |
| openTelemetryClassic | 514.72 | ± 18.22 | ops/s | 8.7x slower |
| openTelemetryExponential | 404.23 | ± 11.87 | ops/s | 11x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToByteArray | 315.39K | ± 4.67K | ops/s | **fastest** |
| prometheusWriteToNull | 312.76K | ± 3.50K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 300.99K | ± 881.91 | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 300.00K | ± 1.10K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      29400.956   ± 1360.965  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1393.187     ± 88.412  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1367.757    ± 140.985  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1304.238     ± 43.522  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      26691.896   ± 1566.576  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      31556.826     ± 33.771  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      31070.323     ± 44.341  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6554.043    ± 179.553  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6949.442    ± 157.977  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6809.859    ± 158.831  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        514.720     ± 18.215  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        404.226     ± 11.872  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       3379.397    ± 183.956  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2186.954    ± 191.438  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4502.986    ± 150.838  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     300001.148   ± 1102.973  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     300991.514    ± 881.911  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     315385.071   ± 4671.797  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     312756.512   ± 3502.504  ops/s
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
