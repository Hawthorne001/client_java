# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-01-31T05:52:42Z
- **Commit:** [`958297d`](https://github.com/Hawthorne001/client_java/commit/958297d5f2802bbe3dc70709b645df557461be9b)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.11.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusNoLabelsInc | 56.20K | ± 1.65K | ops/s | **fastest** |
| prometheusInc | 54.02K | ± 19.75K | ops/s | 1.0x slower |
| prometheusAdd | 51.64K | ± 161.01 | ops/s | 1.1x slower |
| codahaleIncNoLabels | 49.10K | ± 1.81K | ops/s | 1.1x slower |
| simpleclientInc | 6.74K | ± 98.71 | ops/s | 8.3x slower |
| simpleclientNoLabelsInc | 6.45K | ± 11.50 | ops/s | 8.7x slower |
| simpleclientAdd | 6.18K | ± 321.01 | ops/s | 9.1x slower |
| openTelemetryInc | 1.45K | ± 156.94 | ops/s | 39x slower |
| openTelemetryAdd | 1.45K | ± 151.35 | ops/s | 39x slower |
| openTelemetryIncNoLabels | 1.21K | ± 20.93 | ops/s | 46x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.24K | ± 23.35 | ops/s | **fastest** |
| simpleclient | 4.52K | ± 27.61 | ops/s | 1.2x slower |
| prometheusNative | 3.07K | ± 131.74 | ops/s | 1.7x slower |
| openTelemetryClassic | 672.05 | ± 15.72 | ops/s | 7.8x slower |
| openTelemetryExponential | 562.09 | ± 24.64 | ops/s | 9.3x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToByteArray | 531.69K | ± 1.82K | ops/s | **fastest** |
| prometheusWriteToNull | 530.96K | ± 2.93K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 511.44K | ± 4.62K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 506.80K | ± 6.82K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49099.776   ± 1812.287  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1452.801    ± 151.354  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1453.545    ± 156.944  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1212.968     ± 20.927  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51642.208    ± 161.013  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      54016.891  ± 19746.531  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56201.883   ± 1651.827  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6179.808    ± 321.008  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6736.302     ± 98.715  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6448.736     ± 11.495  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        672.054     ± 15.720  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        562.095     ± 24.640  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5240.570     ± 23.347  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3069.160    ± 131.743  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4516.339     ± 27.611  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     506804.151   ± 6820.046  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     511437.493   ± 4618.505  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     531693.105   ± 1823.607  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     530955.817   ± 2934.137  ops/s
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
