# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-02-06T08:51:12Z
- **Commit:** [`586eaf5`](https://github.com/Hawthorne001/client_java/commit/586eaf5298dded8a1eb8add4490736c8a149fcd7)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.11.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 66.00K | ± 1.84K | ops/s | **fastest** |
| prometheusNoLabelsInc | 57.11K | ± 478.88 | ops/s | 1.2x slower |
| prometheusAdd | 51.71K | ± 114.89 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 47.57K | ± 274.33 | ops/s | 1.4x slower |
| simpleclientInc | 6.76K | ± 22.89 | ops/s | 9.8x slower |
| simpleclientNoLabelsInc | 6.48K | ± 144.48 | ops/s | 10x slower |
| simpleclientAdd | 6.27K | ± 172.65 | ops/s | 11x slower |
| openTelemetryAdd | 1.45K | ± 240.48 | ops/s | 45x slower |
| openTelemetryInc | 1.43K | ± 97.45 | ops/s | 46x slower |
| openTelemetryIncNoLabels | 1.34K | ± 48.71 | ops/s | 49x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.63K | ± 67.37 | ops/s | **fastest** |
| simpleclient | 4.59K | ± 30.63 | ops/s | 1.2x slower |
| prometheusNative | 3.06K | ± 113.68 | ops/s | 1.8x slower |
| openTelemetryClassic | 689.94 | ± 46.98 | ops/s | 8.2x slower |
| openTelemetryExponential | 545.61 | ± 13.23 | ops/s | 10x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 532.08K | ± 4.38K | ops/s | **fastest** |
| prometheusWriteToByteArray | 524.40K | ± 8.66K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 488.98K | ± 10.21K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 478.47K | ± 10.55K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      47572.080    ± 274.329  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1450.604    ± 240.477  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1433.977     ± 97.454  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1344.526     ± 48.711  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51711.527    ± 114.893  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      66000.324   ± 1839.898  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      57112.854    ± 478.880  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6270.519    ± 172.651  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6762.311     ± 22.885  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6478.963    ± 144.481  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        689.939     ± 46.981  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        545.609     ± 13.227  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5634.875     ± 67.370  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3062.689    ± 113.675  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4589.583     ± 30.634  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     478469.310  ± 10546.065  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     488975.917  ± 10211.271  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     524403.191   ± 8660.136  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     532081.874   ± 4383.270  ops/s
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
