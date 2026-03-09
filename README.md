# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-03-09T03:20:07Z
- **Commit:** [`e6eb2f9`](https://github.com/Hawthorne001/client_java/commit/e6eb2f91d6da13485a83c4eab5171f510382f800)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.14.0-1017-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 66.10K | ± 673.38 | ops/s | **fastest** |
| prometheusNoLabelsInc | 57.12K | ± 348.93 | ops/s | 1.2x slower |
| prometheusAdd | 51.46K | ± 369.22 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.64K | ± 670.33 | ops/s | 1.4x slower |
| simpleclientInc | 6.76K | ± 29.29 | ops/s | 9.8x slower |
| simpleclientAdd | 6.43K | ± 205.57 | ops/s | 10x slower |
| simpleclientNoLabelsInc | 6.40K | ± 52.41 | ops/s | 10x slower |
| openTelemetryAdd | 1.43K | ± 290.56 | ops/s | 46x slower |
| openTelemetryIncNoLabels | 1.28K | ± 204.68 | ops/s | 51x slower |
| openTelemetryInc | 1.27K | ± 88.92 | ops/s | 52x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 6.16K | ± 1.32K | ops/s | **fastest** |
| simpleclient | 4.52K | ± 15.78 | ops/s | 1.4x slower |
| prometheusNative | 2.91K | ± 293.15 | ops/s | 2.1x slower |
| openTelemetryClassic | 712.63 | ± 33.27 | ops/s | 8.6x slower |
| openTelemetryExponential | 516.06 | ± 14.72 | ops/s | 12x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| openMetricsWriteToNull | 461.07K | ± 4.89K | ops/s | **fastest** |
| prometheusWriteToByteArray | 460.14K | ± 6.76K | ops/s | 1.0x slower |
| prometheusWriteToNull | 458.22K | ± 5.74K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 457.48K | ± 3.80K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48639.354    ± 670.334  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1430.287    ± 290.559  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1272.788     ± 88.922  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1283.696    ± 204.684  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51464.909    ± 369.217  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      66100.773    ± 673.383  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      57122.045    ± 348.933  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6431.911    ± 205.568  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6756.125     ± 29.287  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6400.834     ± 52.405  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        712.632     ± 33.266  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        516.057     ± 14.722  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6161.766   ± 1317.659  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2911.681    ± 293.153  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4522.551     ± 15.779  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     457476.111   ± 3799.482  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     461073.755   ± 4888.813  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     460137.085   ± 6759.152  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     458218.266   ± 5739.360  ops/s
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
