# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-06-11T07:22:37Z
- **Commit:** [`565d168`](https://github.com/Hawthorne001/client_java/commit/565d168cac045b3e7516104b3a22af3bc0014832)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1015-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 59.21K | ± 1.84K | ops/s | **fastest** |
| prometheusNoLabelsInc | 51.15K | ± 401.30 | ops/s | 1.2x slower |
| prometheusAdd | 48.26K | ± 551.00 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 44.07K | ± 297.62 | ops/s | 1.3x slower |
| openTelemetryIncNoLabels | 6.16K | ± 305.07 | ops/s | 9.6x slower |
| simpleclientInc | 6.04K | ± 47.73 | ops/s | 9.8x slower |
| simpleclientNoLabelsInc | 5.91K | ± 20.11 | ops/s | 10x slower |
| simpleclientAdd | 5.66K | ± 517.00 | ops/s | 10x slower |
| openTelemetryAdd | 3.96K | ± 805.79 | ops/s | 15x slower |
| openTelemetryInc | 3.76K | ± 144.64 | ops/s | 16x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 6.18K | ± 3.15K | ops/s | **fastest** |
| simpleclient | 4.26K | ± 33.83 | ops/s | 1.5x slower |
| prometheusNative | 2.81K | ± 245.24 | ops/s | 2.2x slower |
| openTelemetryClassic | 710.85 | ± 14.15 | ops/s | 8.7x slower |
| openTelemetryExponential | 561.99 | ± 39.22 | ops/s | 11x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 27.47K | ± 209.52 | ops/s | **fastest** |
| openMetricsWriteToNull | 27.38K | ± 303.25 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 582.73K | ± 9.46K | ops/s | **fastest** |
| prometheusWriteToByteArray | 568.88K | ± 5.73K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 542.67K | ± 7.23K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 537.25K | ± 2.83K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      44069.875    ± 297.623  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       3964.528    ± 805.795  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       3764.698    ± 144.644  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       6160.547    ± 305.069  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      48258.354    ± 550.996  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      59209.933   ± 1842.771  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      51150.372    ± 401.304  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       5659.131    ± 517.005  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6044.887     ± 47.734  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       5909.107     ± 20.113  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        710.847     ± 14.154  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        561.990     ± 39.218  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6181.463   ± 3151.292  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2814.850    ± 245.239  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4255.153     ± 33.827  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      27382.093    ± 303.255  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      27468.107    ± 209.519  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     537245.662   ± 2825.111  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     542670.121   ± 7226.521  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     568882.034   ± 5729.076  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     582734.217   ± 9463.192  ops/s
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
