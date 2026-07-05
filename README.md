# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-07-04T11:18:50Z
- **Commit:** [`7f899e7`](https://github.com/Hawthorne001/client_java/commit/7f899e79ded325256bd0e444e33696b5f194700d)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 64.01K | ± 3.31K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.66K | ± 326.59 | ops/s | 1.1x slower |
| prometheusAdd | 51.12K | ± 804.65 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.71K | ± 1.14K | ops/s | 1.3x slower |
| simpleclientInc | 6.53K | ± 48.16 | ops/s | 9.8x slower |
| simpleclientAdd | 6.44K | ± 19.06 | ops/s | 9.9x slower |
| simpleclientNoLabelsInc | 6.34K | ± 17.60 | ops/s | 10x slower |
| openTelemetryAdd | 3.38K | ± 264.42 | ops/s | 19x slower |
| openTelemetryIncNoLabels | 3.03K | ± 33.92 | ops/s | 21x slower |
| openTelemetryInc | 2.91K | ± 50.41 | ops/s | 22x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| simpleclient | 4.37K | ± 41.26 | ops/s | **fastest** |
| prometheusClassic | 4.09K | ± 80.06 | ops/s | 1.1x slower |
| prometheusNative | 3.23K | ± 163.94 | ops/s | 1.4x slower |
| openTelemetryClassic | 760.31 | ± 25.09 | ops/s | 5.8x slower |
| openTelemetryExponential | 628.76 | ± 77.18 | ops/s | 7.0x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| openMetricsWriteToNull | 24.03K | ± 1.22K | ops/s | **fastest** |
| prometheusWriteToNull | 23.43K | ± 969.96 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 515.52K | ± 6.15K | ops/s | **fastest** |
| prometheusWriteToByteArray | 513.74K | ± 7.52K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 495.37K | ± 1.52K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 495.27K | ± 2.76K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48705.744   ± 1137.981  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       3375.644    ± 264.416  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       2909.391     ± 50.405  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       3031.200     ± 33.923  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51115.830    ± 804.646  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      64012.472   ± 3305.982  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56662.819    ± 326.587  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6444.514     ± 19.064  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6529.586     ± 48.163  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6336.953     ± 17.604  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        760.313     ± 25.086  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        628.757     ± 77.179  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       4094.449     ± 80.062  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3232.689    ± 163.944  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4372.722     ± 41.265  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      24027.216   ± 1219.106  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      23434.922    ± 969.958  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     495371.901   ± 1524.341  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     495272.969   ± 2760.623  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     513738.007   ± 7519.883  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     515524.110   ± 6152.689  ops/s
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
