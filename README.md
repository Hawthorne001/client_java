# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-05-03T11:21:29Z
- **Commit:** [`188e434`](https://github.com/Hawthorne001/client_java/commit/188e434f25be73f75a463239b5cb4d54a8f72cca)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** Intel(R) Xeon(R) Platinum 8370C CPU @ 2.80GHz, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1010-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusNoLabelsInc | 30.61K | ± 1.49K | ops/s | **fastest** |
| codahaleIncNoLabels | 30.26K | ± 1.71K | ops/s | 1.0x slower |
| prometheusInc | 29.89K | ± 1.32K | ops/s | 1.0x slower |
| prometheusAdd | 27.90K | ± 863.31 | ops/s | 1.1x slower |
| simpleclientInc | 6.77K | ± 252.03 | ops/s | 4.5x slower |
| simpleclientNoLabelsInc | 6.75K | ± 171.12 | ops/s | 4.5x slower |
| simpleclientAdd | 6.67K | ± 110.26 | ops/s | 4.6x slower |
| openTelemetryIncNoLabels | 2.57K | ± 242.30 | ops/s | 12x slower |
| openTelemetryInc | 2.45K | ± 140.18 | ops/s | 12x slower |
| openTelemetryAdd | 2.35K | ± 116.89 | ops/s | 13x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| simpleclient | 4.34K | ± 110.26 | ops/s | **fastest** |
| prometheusClassic | 3.50K | ± 1.72K | ops/s | 1.2x slower |
| prometheusNative | 2.37K | ± 231.61 | ops/s | 1.8x slower |
| openTelemetryClassic | 604.91 | ± 6.45 | ops/s | 7.2x slower |
| openTelemetryExponential | 432.94 | ± 9.35 | ops/s | 10x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 315.52K | ± 1.12K | ops/s | **fastest** |
| prometheusWriteToByteArray | 313.29K | ± 1.65K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 295.81K | ± 1.23K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 293.87K | ± 784.08 | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      30255.353   ± 1712.635  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       2353.191    ± 116.889  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       2452.611    ± 140.184  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       2568.882    ± 242.297  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      27898.198    ± 863.313  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      29887.376   ± 1315.633  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      30611.507   ± 1487.800  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6667.251    ± 110.259  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6765.144    ± 252.026  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6752.358    ± 171.121  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        604.907      ± 6.445  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        432.937      ± 9.348  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       3500.412   ± 1724.211  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2370.218    ± 231.609  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4342.337    ± 110.260  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     293874.244    ± 784.082  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     295807.024   ± 1225.356  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     313291.445   ± 1652.157  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     315524.975   ± 1116.179  ops/s
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
