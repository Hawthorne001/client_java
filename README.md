# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-04-19T00:44:42Z
- **Commit:** [`4b69f40`](https://github.com/Hawthorne001/client_java/commit/4b69f40bd4e616d69468ce99dc4323162287a577)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1010-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.13K | ± 2.53K | ops/s | **fastest** |
| prometheusNoLabelsInc | 57.20K | ± 569.83 | ops/s | 1.1x slower |
| prometheusAdd | 50.99K | ± 625.90 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 49.47K | ± 2.03K | ops/s | 1.3x slower |
| simpleclientInc | 6.47K | ± 183.54 | ops/s | 10x slower |
| simpleclientNoLabelsInc | 6.37K | ± 207.39 | ops/s | 10x slower |
| simpleclientAdd | 6.29K | ± 263.22 | ops/s | 10x slower |
| openTelemetryInc | 1.39K | ± 328.49 | ops/s | 47x slower |
| openTelemetryAdd | 1.27K | ± 73.03 | ops/s | 51x slower |
| openTelemetryIncNoLabels | 1.26K | ± 74.75 | ops/s | 52x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 6.13K | ± 1.75K | ops/s | **fastest** |
| simpleclient | 4.39K | ± 17.16 | ops/s | 1.4x slower |
| prometheusNative | 2.99K | ± 238.03 | ops/s | 2.1x slower |
| openTelemetryClassic | 692.91 | ± 20.46 | ops/s | 8.8x slower |
| openTelemetryExponential | 561.17 | ± 15.52 | ops/s | 11x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 491.47K | ± 921.10 | ops/s | **fastest** |
| prometheusWriteToByteArray | 485.74K | ± 3.57K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 471.58K | ± 5.44K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 469.42K | ± 2.77K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49468.647   ± 2028.214  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1266.875     ± 73.031  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1393.210    ± 328.490  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1259.845     ± 74.752  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      50986.395    ± 625.903  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65131.637   ± 2526.942  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      57200.991    ± 569.830  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6289.817    ± 263.219  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6466.485    ± 183.544  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6367.487    ± 207.393  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        692.915     ± 20.456  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        561.167     ± 15.518  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6129.586   ± 1754.265  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2985.633    ± 238.027  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4388.289     ± 17.161  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     469419.414   ± 2765.597  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     471577.791   ± 5444.943  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     485740.096   ± 3572.123  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     491471.978    ± 921.099  ops/s
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
