# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-04-16T22:35:46Z
- **Commit:** [`4b69f40`](https://github.com/Hawthorne001/client_java/commit/4b69f40bd4e616d69468ce99dc4323162287a577)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1010-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.38K | ± 2.32K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.27K | ± 1.45K | ops/s | 1.2x slower |
| prometheusAdd | 51.43K | ± 306.35 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 49.87K | ± 2.03K | ops/s | 1.3x slower |
| simpleclientInc | 6.46K | ± 202.10 | ops/s | 10x slower |
| simpleclientNoLabelsInc | 6.38K | ± 236.24 | ops/s | 10x slower |
| simpleclientAdd | 6.28K | ± 255.50 | ops/s | 10x slower |
| openTelemetryInc | 1.36K | ± 167.23 | ops/s | 48x slower |
| openTelemetryAdd | 1.22K | ± 113.64 | ops/s | 54x slower |
| openTelemetryIncNoLabels | 1.19K | ± 59.46 | ops/s | 55x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.03K | ± 1.49K | ops/s | **fastest** |
| simpleclient | 4.43K | ± 63.44 | ops/s | 1.1x slower |
| prometheusNative | 2.75K | ± 333.15 | ops/s | 1.8x slower |
| openTelemetryClassic | 681.17 | ± 12.68 | ops/s | 7.4x slower |
| openTelemetryExponential | 561.87 | ± 20.39 | ops/s | 9.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 456.56K | ± 24.73K | ops/s | **fastest** |
| prometheusWriteToByteArray | 449.76K | ± 23.01K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 445.21K | ± 22.45K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 437.06K | ± 11.67K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49868.872   ± 2032.714  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1215.489    ± 113.643  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1363.164    ± 167.234  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1190.153     ± 59.461  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51425.642    ± 306.350  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65377.751   ± 2316.924  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56269.414   ± 1446.228  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6280.232    ± 255.496  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6457.742    ± 202.104  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6380.473    ± 236.239  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        681.168     ± 12.675  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        561.870     ± 20.389  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5030.448   ± 1487.140  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2753.494    ± 333.151  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4426.048     ± 63.445  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     437058.036  ± 11668.909  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     445212.972  ± 22454.168  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     449759.327  ± 23011.733  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     456558.053  ± 24734.263  ops/s
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
