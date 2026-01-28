# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-01-28T03:58:33Z
- **Commit:** [`d32fd12`](https://github.com/Hawthorne001/client_java/commit/d32fd1260440996d672c2650d43af3b535a28c32)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.11.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.97K | ± 139.48 | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.57K | ± 690.49 | ops/s | 1.2x slower |
| prometheusAdd | 51.19K | ± 725.55 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 49.51K | ± 691.38 | ops/s | 1.3x slower |
| simpleclientInc | 6.64K | ± 204.92 | ops/s | 9.9x slower |
| simpleclientNoLabelsInc | 6.59K | ± 199.57 | ops/s | 10x slower |
| simpleclientAdd | 6.44K | ± 189.75 | ops/s | 10x slower |
| openTelemetryInc | 1.26K | ± 36.87 | ops/s | 52x slower |
| openTelemetryAdd | 1.26K | ± 53.62 | ops/s | 52x slower |
| openTelemetryIncNoLabels | 1.23K | ± 23.26 | ops/s | 54x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.34K | ± 126.69 | ops/s | **fastest** |
| simpleclient | 4.50K | ± 104.59 | ops/s | 1.2x slower |
| prometheusNative | 3.03K | ± 136.52 | ops/s | 1.8x slower |
| openTelemetryClassic | 679.76 | ± 57.04 | ops/s | 7.9x slower |
| openTelemetryExponential | 516.54 | ± 17.83 | ops/s | 10x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 550.49K | ± 6.67K | ops/s | **fastest** |
| prometheusWriteToByteArray | 536.25K | ± 2.10K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 519.39K | ± 4.77K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 519.32K | ± 4.05K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49512.674    ± 691.383  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1260.793     ± 53.615  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1262.921     ± 36.869  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1225.177     ± 23.256  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51187.526    ± 725.548  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65973.943    ± 139.485  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56569.156    ± 690.491  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6435.228    ± 189.755  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6635.013    ± 204.921  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6591.532    ± 199.572  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        679.759     ± 57.044  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        516.541     ± 17.834  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5343.329    ± 126.686  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3028.841    ± 136.522  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4495.233    ± 104.588  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     519322.331   ± 4054.875  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     519391.656   ± 4771.297  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     536251.351   ± 2098.049  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     550493.338   ± 6673.170  ops/s
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
