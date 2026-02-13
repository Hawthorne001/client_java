# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-02-13T13:50:48Z
- **Commit:** [`09bbeee`](https://github.com/Hawthorne001/client_java/commit/09bbeee1225edb7d7e4acb6c4525c9c53fb2e613)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.14.0-1017-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.97K | ± 114.05 | ops/s | **fastest** |
| prometheusNoLabelsInc | 57.00K | ± 416.04 | ops/s | 1.2x slower |
| prometheusAdd | 51.49K | ± 86.16 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.60K | ± 1.38K | ops/s | 1.4x slower |
| simpleclientInc | 6.76K | ± 34.25 | ops/s | 9.8x slower |
| simpleclientNoLabelsInc | 6.70K | ± 13.89 | ops/s | 9.9x slower |
| simpleclientAdd | 6.34K | ± 192.88 | ops/s | 10x slower |
| openTelemetryIncNoLabels | 1.39K | ± 152.41 | ops/s | 47x slower |
| openTelemetryAdd | 1.27K | ± 77.98 | ops/s | 52x slower |
| openTelemetryInc | 1.25K | ± 114.31 | ops/s | 53x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 6.37K | ± 1.61K | ops/s | **fastest** |
| simpleclient | 4.56K | ± 62.11 | ops/s | 1.4x slower |
| prometheusNative | 3.07K | ± 286.58 | ops/s | 2.1x slower |
| openTelemetryClassic | 705.71 | ± 43.05 | ops/s | 9.0x slower |
| openTelemetryExponential | 556.02 | ± 20.48 | ops/s | 11x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToByteArray | 485.77K | ± 3.26K | ops/s | **fastest** |
| prometheusWriteToNull | 484.30K | ± 6.05K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 477.13K | ± 2.24K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 465.61K | ± 9.51K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48596.889   ± 1381.484  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1273.343     ± 77.983  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1249.794    ± 114.310  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1393.140    ± 152.410  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51487.250     ± 86.163  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65968.527    ± 114.053  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56999.200    ± 416.043  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6336.356    ± 192.881  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6757.612     ± 34.250  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6696.489     ± 13.885  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        705.710     ± 43.048  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        556.022     ± 20.479  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6370.573   ± 1614.505  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3072.941    ± 286.578  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4562.992     ± 62.105  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     465609.023   ± 9514.469  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     477130.945   ± 2238.188  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     485770.907   ± 3258.522  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     484301.910   ± 6053.874  ops/s
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
