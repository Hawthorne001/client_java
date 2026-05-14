# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-05-14T16:12:30Z
- **Commit:** [`63f82ad`](https://github.com/Hawthorne001/client_java/commit/63f82addfc2f5fc81bdabfbc49ddbc0ecb2874b8)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1010-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 60.57K | ± 614.16 | ops/s | **fastest** |
| prometheusNoLabelsInc | 51.47K | ± 901.10 | ops/s | 1.2x slower |
| prometheusAdd | 48.24K | ± 297.50 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 43.89K | ± 86.62 | ops/s | 1.4x slower |
| simpleclientInc | 6.14K | ± 56.22 | ops/s | 9.9x slower |
| simpleclientNoLabelsInc | 5.89K | ± 45.84 | ops/s | 10x slower |
| simpleclientAdd | 5.76K | ± 100.60 | ops/s | 11x slower |
| openTelemetryIncNoLabels | 4.65K | ± 1.24K | ops/s | 13x slower |
| openTelemetryInc | 4.46K | ± 916.43 | ops/s | 14x slower |
| openTelemetryAdd | 4.40K | ± 836.92 | ops/s | 14x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 4.63K | ± 346.13 | ops/s | **fastest** |
| simpleclient | 4.37K | ± 26.87 | ops/s | 1.1x slower |
| prometheusNative | 2.95K | ± 285.68 | ops/s | 1.6x slower |
| openTelemetryClassic | 716.45 | ± 20.13 | ops/s | 6.5x slower |
| openTelemetryExponential | 555.93 | ± 8.74 | ops/s | 8.3x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 27.59K | ± 200.38 | ops/s | **fastest** |
| openMetricsWriteToNull | 27.17K | ± 376.87 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 586.74K | ± 6.75K | ops/s | **fastest** |
| prometheusWriteToByteArray | 563.04K | ± 8.25K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 540.23K | ± 12.80K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 522.21K | ± 6.74K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      43888.064     ± 86.619  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       4399.309    ± 836.921  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       4459.261    ± 916.434  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       4647.980   ± 1243.315  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      48238.328    ± 297.505  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      60572.321    ± 614.161  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      51469.972    ± 901.102  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       5758.417    ± 100.602  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6137.327     ± 56.223  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       5890.680     ± 45.842  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        716.452     ± 20.130  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        555.928      ± 8.745  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       4630.571    ± 346.129  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2947.110    ± 285.678  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4369.805     ± 26.866  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      27168.806    ± 376.871  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      27588.934    ± 200.384  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     522213.124   ± 6742.263  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     540231.612  ± 12798.342  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     563036.414   ± 8251.045  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     586736.015   ± 6750.634  ops/s
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
