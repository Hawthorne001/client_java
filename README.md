# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-03-03T23:13:48Z
- **Commit:** [`7fe2528`](https://github.com/Hawthorne001/client_java/commit/7fe2528a85574ff6ae35e539039619c4a6db7231)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.14.0-1017-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 61.49K | ± 8.11K | ops/s | **fastest** |
| prometheusNoLabelsInc | 57.25K | ± 158.33 | ops/s | 1.1x slower |
| prometheusAdd | 51.25K | ± 717.42 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 43.62K | ± 7.85K | ops/s | 1.4x slower |
| simpleclientNoLabelsInc | 6.70K | ± 22.01 | ops/s | 9.2x slower |
| simpleclientInc | 6.64K | ± 236.27 | ops/s | 9.3x slower |
| simpleclientAdd | 6.28K | ± 207.32 | ops/s | 9.8x slower |
| openTelemetryAdd | 1.49K | ± 263.30 | ops/s | 41x slower |
| openTelemetryIncNoLabels | 1.32K | ± 171.15 | ops/s | 47x slower |
| openTelemetryInc | 1.16K | ± 31.62 | ops/s | 53x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 6.45K | ± 734.73 | ops/s | **fastest** |
| simpleclient | 4.52K | ± 27.11 | ops/s | 1.4x slower |
| prometheusNative | 2.95K | ± 335.00 | ops/s | 2.2x slower |
| openTelemetryClassic | 684.35 | ± 50.84 | ops/s | 9.4x slower |
| openTelemetryExponential | 559.21 | ± 31.79 | ops/s | 12x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 492.47K | ± 4.87K | ops/s | **fastest** |
| prometheusWriteToByteArray | 488.06K | ± 2.39K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 485.23K | ± 3.10K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 483.55K | ± 2.74K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      43624.046   ± 7847.521  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1494.456    ± 263.296  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1155.783     ± 31.622  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1320.291    ± 171.149  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51251.950    ± 717.420  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      61490.022   ± 8105.735  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      57245.505    ± 158.328  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6279.425    ± 207.319  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6636.789    ± 236.268  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6695.969     ± 22.005  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        684.355     ± 50.838  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        559.213     ± 31.792  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6450.044    ± 734.725  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2952.160    ± 335.000  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4517.400     ± 27.110  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     483554.896   ± 2737.001  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     485228.488   ± 3103.030  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     488061.546   ± 2390.544  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     492467.374   ± 4873.364  ops/s
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
