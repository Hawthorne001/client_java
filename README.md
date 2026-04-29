# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-04-29T08:54:09Z
- **Commit:** [`fa68aa7`](https://github.com/Hawthorne001/client_java/commit/fa68aa7789c53d54ea1783f120194a3feae7e7b8)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1010-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.26K | ± 1.31K | ops/s | **fastest** |
| prometheusNoLabelsInc | 57.06K | ± 77.29 | ops/s | 1.1x slower |
| prometheusAdd | 50.85K | ± 702.55 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 50.17K | ± 94.34 | ops/s | 1.3x slower |
| simpleclientInc | 6.43K | ± 183.19 | ops/s | 10x slower |
| simpleclientNoLabelsInc | 6.43K | ± 144.26 | ops/s | 10x slower |
| simpleclientAdd | 6.20K | ± 210.67 | ops/s | 11x slower |
| openTelemetryIncNoLabels | 3.19K | ± 41.73 | ops/s | 20x slower |
| openTelemetryInc | 3.15K | ± 46.38 | ops/s | 21x slower |
| openTelemetryAdd | 3.13K | ± 150.55 | ops/s | 21x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.50K | ± 1.21K | ops/s | **fastest** |
| simpleclient | 4.48K | ± 31.53 | ops/s | 1.2x slower |
| prometheusNative | 3.08K | ± 176.03 | ops/s | 1.8x slower |
| openTelemetryExponential | 749.51 | ± 54.00 | ops/s | 7.3x slower |
| openTelemetryClassic | 732.32 | ± 17.31 | ops/s | 7.5x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| openMetricsWriteToByteArray | 464.06K | ± 5.32K | ops/s | **fastest** |
| prometheusWriteToNull | 462.41K | ± 5.26K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 460.55K | ± 8.60K | ops/s | 1.0x slower |
| prometheusWriteToByteArray | 458.21K | ± 20.39K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      50171.909     ± 94.342  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       3130.825    ± 150.548  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       3152.695     ± 46.381  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       3192.523     ± 41.733  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      50854.823    ± 702.549  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65261.388   ± 1313.414  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      57057.210     ± 77.292  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6204.164    ± 210.667  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6433.348    ± 183.193  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6430.916    ± 144.255  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        732.318     ± 17.309  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        749.509     ± 54.000  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5504.054   ± 1209.490  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3081.448    ± 176.027  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4483.760     ± 31.530  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     464057.795   ± 5318.792  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     460550.918   ± 8599.737  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     458212.390  ± 20386.922  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     462410.736   ± 5264.894  ops/s
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
