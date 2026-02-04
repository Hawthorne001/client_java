# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-02-04T07:35:58Z
- **Commit:** [`1f3865f`](https://github.com/Hawthorne001/client_java/commit/1f3865fd7a03f8e835795117f835ab99f675f67e)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.11.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 66.49K | ± 874.53 | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.45K | ± 1.20K | ops/s | 1.2x slower |
| prometheusAdd | 51.55K | ± 262.24 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.46K | ± 2.54K | ops/s | 1.4x slower |
| simpleclientNoLabelsInc | 6.62K | ± 138.39 | ops/s | 10x slower |
| simpleclientInc | 6.61K | ± 135.51 | ops/s | 10x slower |
| simpleclientAdd | 6.41K | ± 240.29 | ops/s | 10x slower |
| openTelemetryInc | 1.35K | ± 165.69 | ops/s | 49x slower |
| openTelemetryIncNoLabels | 1.34K | ± 124.79 | ops/s | 50x slower |
| openTelemetryAdd | 1.27K | ± 40.29 | ops/s | 52x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.28K | ± 47.18 | ops/s | **fastest** |
| simpleclient | 4.56K | ± 49.35 | ops/s | 1.2x slower |
| prometheusNative | 3.01K | ± 221.38 | ops/s | 1.8x slower |
| openTelemetryClassic | 657.80 | ± 49.56 | ops/s | 8.0x slower |
| openTelemetryExponential | 567.53 | ± 28.11 | ops/s | 9.3x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 532.81K | ± 13.36K | ops/s | **fastest** |
| prometheusWriteToByteArray | 522.92K | ± 11.22K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 515.70K | ± 7.13K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 509.29K | ± 5.95K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48462.648   ± 2544.885  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1268.145     ± 40.289  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1354.144    ± 165.686  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1340.418    ± 124.787  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51552.109    ± 262.242  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      66487.185    ± 874.530  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56445.069   ± 1199.335  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6411.576    ± 240.286  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6608.397    ± 135.513  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6622.998    ± 138.389  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        657.799     ± 49.555  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        567.530     ± 28.110  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5279.863     ± 47.183  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3011.384    ± 221.383  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4557.443     ± 49.350  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     509289.102   ± 5950.772  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     515698.258   ± 7127.008  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     522917.429  ± 11224.855  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     532812.512  ± 13355.282  ops/s
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
