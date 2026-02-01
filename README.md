# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-02-01T06:25:27Z
- **Commit:** [`421033a`](https://github.com/Hawthorne001/client_java/commit/421033a2f72ef0c52d77fae6eb1b346c81b1fdb3)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.11.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.14K | ± 1.19K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.38K | ± 937.93 | ops/s | 1.2x slower |
| prometheusAdd | 51.09K | ± 249.52 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 49.45K | ± 801.57 | ops/s | 1.3x slower |
| simpleclientInc | 6.72K | ± 55.85 | ops/s | 9.7x slower |
| simpleclientNoLabelsInc | 6.68K | ± 41.93 | ops/s | 9.8x slower |
| simpleclientAdd | 6.34K | ± 315.15 | ops/s | 10x slower |
| openTelemetryIncNoLabels | 1.38K | ± 175.66 | ops/s | 47x slower |
| openTelemetryAdd | 1.36K | ± 28.89 | ops/s | 48x slower |
| openTelemetryInc | 1.26K | ± 16.77 | ops/s | 52x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.34K | ± 269.33 | ops/s | **fastest** |
| simpleclient | 4.53K | ± 43.00 | ops/s | 1.2x slower |
| prometheusNative | 2.90K | ± 89.73 | ops/s | 1.8x slower |
| openTelemetryClassic | 680.39 | ± 16.26 | ops/s | 7.9x slower |
| openTelemetryExponential | 546.03 | ± 17.28 | ops/s | 9.8x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 527.20K | ± 7.68K | ops/s | **fastest** |
| prometheusWriteToByteArray | 527.20K | ± 5.56K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 509.66K | ± 783.61 | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 506.19K | ± 7.85K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49449.438    ± 801.574  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1358.809     ± 28.895  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1257.478     ± 16.773  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1380.032    ± 175.663  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51092.601    ± 249.523  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65144.161   ± 1191.475  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56379.933    ± 937.934  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6341.846    ± 315.150  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6722.890     ± 55.852  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6681.167     ± 41.932  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        680.389     ± 16.264  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        546.027     ± 17.281  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5343.940    ± 269.326  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2898.907     ± 89.733  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4528.100     ± 43.003  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     506185.398   ± 7848.724  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     509660.190    ± 783.606  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     527195.387   ± 5562.420  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     527204.004   ± 7683.138  ops/s
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
