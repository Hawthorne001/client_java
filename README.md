# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-02-23T17:06:50Z
- **Commit:** [`f645a80`](https://github.com/Hawthorne001/client_java/commit/f645a80f239985098f703c3a542ba534e28e04de)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** Intel(R) Xeon(R) Platinum 8370C CPU @ 2.80GHz, 4 cores, 16 GB RAM
- **OS:** Linux 6.11.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 31.46K | ± 205.91 | ops/s | **fastest** |
| codahaleIncNoLabels | 30.84K | ± 178.42 | ops/s | 1.0x slower |
| prometheusNoLabelsInc | 29.98K | ± 730.79 | ops/s | 1.0x slower |
| prometheusAdd | 28.17K | ± 543.56 | ops/s | 1.1x slower |
| simpleclientInc | 6.98K | ± 154.35 | ops/s | 4.5x slower |
| simpleclientNoLabelsInc | 6.94K | ± 138.30 | ops/s | 4.5x slower |
| simpleclientAdd | 6.85K | ± 29.55 | ops/s | 4.6x slower |
| openTelemetryIncNoLabels | 1.49K | ± 129.10 | ops/s | 21x slower |
| openTelemetryAdd | 1.38K | ± 65.91 | ops/s | 23x slower |
| openTelemetryInc | 1.33K | ± 49.76 | ops/s | 24x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| simpleclient | 4.52K | ± 108.03 | ops/s | **fastest** |
| prometheusClassic | 2.63K | ± 147.02 | ops/s | 1.7x slower |
| prometheusNative | 2.08K | ± 229.78 | ops/s | 2.2x slower |
| openTelemetryClassic | 500.23 | ± 17.08 | ops/s | 9.0x slower |
| openTelemetryExponential | 393.25 | ± 7.83 | ops/s | 12x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 319.55K | ± 1.34K | ops/s | **fastest** |
| prometheusWriteToByteArray | 315.14K | ± 1.63K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 301.96K | ± 1.73K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 297.12K | ± 1.82K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      30844.094    ± 178.416  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1384.388     ± 65.907  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1332.741     ± 49.757  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1487.150    ± 129.097  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      28166.895    ± 543.557  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      31459.054    ± 205.911  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      29980.361    ± 730.791  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6854.944     ± 29.550  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6978.533    ± 154.348  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6943.185    ± 138.303  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        500.229     ± 17.080  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        393.247      ± 7.833  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       2630.503    ± 147.018  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2078.325    ± 229.784  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4522.414    ± 108.026  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     297119.572   ± 1820.552  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     301956.337   ± 1725.213  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     315141.114   ± 1632.402  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     319548.481   ± 1342.373  ops/s
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
