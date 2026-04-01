# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-04-01T15:00:41Z
- **Commit:** [`deb782f`](https://github.com/Hawthorne001/client_java/commit/deb782f9fce60ffb1308a98b661c0a1ccb79a82b)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1008-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.46K | ± 2.22K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.91K | ± 384.71 | ops/s | 1.2x slower |
| prometheusAdd | 51.55K | ± 246.53 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 49.35K | ± 1.50K | ops/s | 1.3x slower |
| simpleclientNoLabelsInc | 6.58K | ± 31.54 | ops/s | 9.9x slower |
| simpleclientInc | 6.54K | ± 217.73 | ops/s | 10x slower |
| simpleclientAdd | 6.01K | ± 154.27 | ops/s | 11x slower |
| openTelemetryInc | 1.27K | ± 7.36 | ops/s | 51x slower |
| openTelemetryIncNoLabels | 1.27K | ± 27.40 | ops/s | 52x slower |
| openTelemetryAdd | 1.26K | ± 21.41 | ops/s | 52x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 6.26K | ± 2.07K | ops/s | **fastest** |
| simpleclient | 4.45K | ± 14.11 | ops/s | 1.4x slower |
| prometheusNative | 2.80K | ± 298.22 | ops/s | 2.2x slower |
| openTelemetryClassic | 707.88 | ± 36.24 | ops/s | 8.8x slower |
| openTelemetryExponential | 569.27 | ± 32.74 | ops/s | 11x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToByteArray | 474.72K | ± 3.19K | ops/s | **fastest** |
| prometheusWriteToNull | 470.48K | ± 6.61K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 456.78K | ± 4.93K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 438.09K | ± 18.13K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49351.750   ± 1498.554  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1257.055     ± 21.409  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1272.131      ± 7.360  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1270.944     ± 27.403  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51551.315    ± 246.532  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65460.746   ± 2224.236  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56909.085    ± 384.712  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6006.464    ± 154.268  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6537.265    ± 217.728  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6581.470     ± 31.545  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        707.884     ± 36.243  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        569.267     ± 32.744  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6258.625   ± 2074.925  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2804.013    ± 298.218  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4449.991     ± 14.111  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     438086.968  ± 18130.917  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     456782.134   ± 4933.775  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     474724.519   ± 3188.225  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     470478.889   ± 6606.473  ops/s
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
