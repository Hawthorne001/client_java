# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-04-22T03:49:14Z
- **Commit:** [`4b69f40`](https://github.com/Hawthorne001/client_java/commit/4b69f40bd4e616d69468ce99dc4323162287a577)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1011-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.16K | ± 923.61 | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.99K | ± 486.34 | ops/s | 1.1x slower |
| prometheusAdd | 50.99K | ± 699.72 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.96K | ± 1.00K | ops/s | 1.3x slower |
| simpleclientInc | 6.59K | ± 153.69 | ops/s | 9.9x slower |
| simpleclientNoLabelsInc | 6.52K | ± 133.41 | ops/s | 10.0x slower |
| simpleclientAdd | 6.11K | ± 257.31 | ops/s | 11x slower |
| openTelemetryAdd | 1.48K | ± 332.23 | ops/s | 44x slower |
| openTelemetryIncNoLabels | 1.37K | ± 144.43 | ops/s | 48x slower |
| openTelemetryInc | 1.23K | ± 34.93 | ops/s | 53x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 4.52K | ± 455.56 | ops/s | **fastest** |
| simpleclient | 4.45K | ± 75.33 | ops/s | 1.0x slower |
| prometheusNative | 2.72K | ± 199.80 | ops/s | 1.7x slower |
| openTelemetryClassic | 668.87 | ± 40.72 | ops/s | 6.8x slower |
| openTelemetryExponential | 535.29 | ± 34.50 | ops/s | 8.4x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 482.81K | ± 2.55K | ops/s | **fastest** |
| prometheusWriteToByteArray | 471.65K | ± 4.58K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 470.21K | ± 5.68K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 462.90K | ± 4.19K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48955.787   ± 1003.622  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1476.556    ± 332.235  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1227.849     ± 34.932  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1365.951    ± 144.433  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      50992.890    ± 699.719  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65164.069    ± 923.606  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56994.453    ± 486.335  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6112.674    ± 257.306  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6586.344    ± 153.686  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6518.282    ± 133.407  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        668.865     ± 40.718  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        535.291     ± 34.496  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       4516.415    ± 455.562  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2723.015    ± 199.795  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4445.950     ± 75.328  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     462898.874   ± 4185.441  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     470208.719   ± 5675.160  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     471653.781   ± 4579.546  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     482814.977   ± 2554.567  ops/s
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
