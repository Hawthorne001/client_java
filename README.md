# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-05-30T04:26:11Z
- **Commit:** [`f0a3b2e`](https://github.com/Hawthorne001/client_java/commit/f0a3b2e46296428952756c95c9037982e7e9baa7)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1015-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 59.87K | ± 1.04K | ops/s | **fastest** |
| prometheusNoLabelsInc | 51.55K | ± 647.67 | ops/s | 1.2x slower |
| prometheusAdd | 48.69K | ± 944.56 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 42.98K | ± 1.79K | ops/s | 1.4x slower |
| simpleclientInc | 6.16K | ± 66.27 | ops/s | 9.7x slower |
| simpleclientAdd | 6.03K | ± 154.06 | ops/s | 9.9x slower |
| simpleclientNoLabelsInc | 5.90K | ± 16.09 | ops/s | 10x slower |
| openTelemetryIncNoLabels | 4.79K | ± 1.15K | ops/s | 12x slower |
| openTelemetryInc | 4.50K | ± 972.65 | ops/s | 13x slower |
| openTelemetryAdd | 3.89K | ± 734.25 | ops/s | 15x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| simpleclient | 4.52K | ± 40.60 | ops/s | **fastest** |
| prometheusClassic | 3.96K | ± 173.20 | ops/s | 1.1x slower |
| prometheusNative | 3.02K | ± 167.00 | ops/s | 1.5x slower |
| openTelemetryClassic | 708.32 | ± 6.58 | ops/s | 6.4x slower |
| openTelemetryExponential | 547.68 | ± 10.40 | ops/s | 8.3x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 27.59K | ± 327.96 | ops/s | **fastest** |
| openMetricsWriteToNull | 27.19K | ± 239.14 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 585.73K | ± 8.07K | ops/s | **fastest** |
| prometheusWriteToByteArray | 572.36K | ± 7.36K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 552.46K | ± 3.74K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 540.93K | ± 4.57K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      42976.249   ± 1791.103  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       3887.014    ± 734.253  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       4496.058    ± 972.653  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       4793.385   ± 1150.280  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      48693.605    ± 944.564  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      59867.432   ± 1036.475  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      51554.554    ± 647.668  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6034.229    ± 154.058  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6162.788     ± 66.267  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       5902.081     ± 16.088  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        708.319      ± 6.580  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        547.683     ± 10.396  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       3961.474    ± 173.203  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3022.195    ± 167.004  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4520.747     ± 40.603  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      27185.654    ± 239.136  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      27593.331    ± 327.958  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     540934.577   ± 4572.394  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     552463.072   ± 3738.876  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     572359.638   ± 7359.902  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     585726.220   ± 8072.530  ops/s
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
