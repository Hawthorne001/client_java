# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-02-15T14:34:47Z
- **Commit:** [`043fc57`](https://github.com/Hawthorne001/client_java/commit/043fc5742752fdc2f67f0219418030a190c53bde)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.14.0-1017-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.48K | ± 1.53K | ops/s | **fastest** |
| prometheusNoLabelsInc | 55.16K | ± 2.71K | ops/s | 1.2x slower |
| prometheusAdd | 50.04K | ± 1.10K | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.89K | ± 1.11K | ops/s | 1.3x slower |
| simpleclientInc | 6.66K | ± 140.23 | ops/s | 9.8x slower |
| simpleclientNoLabelsInc | 6.47K | ± 200.91 | ops/s | 10x slower |
| simpleclientAdd | 6.11K | ± 422.84 | ops/s | 11x slower |
| openTelemetryAdd | 1.47K | ± 233.82 | ops/s | 45x slower |
| openTelemetryInc | 1.45K | ± 154.70 | ops/s | 45x slower |
| openTelemetryIncNoLabels | 1.25K | ± 23.47 | ops/s | 52x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.04K | ± 811.51 | ops/s | **fastest** |
| simpleclient | 4.57K | ± 37.67 | ops/s | 1.1x slower |
| prometheusNative | 2.98K | ± 327.63 | ops/s | 1.7x slower |
| openTelemetryClassic | 703.91 | ± 48.27 | ops/s | 7.2x slower |
| openTelemetryExponential | 550.37 | ± 28.84 | ops/s | 9.2x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 498.14K | ± 1.62K | ops/s | **fastest** |
| prometheusWriteToByteArray | 497.45K | ± 2.35K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 492.31K | ± 2.54K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 488.59K | ± 4.35K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48894.746   ± 1108.397  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1466.049    ± 233.818  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1454.195    ± 154.697  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1248.756     ± 23.471  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      50043.900   ± 1096.906  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65478.586   ± 1530.102  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      55164.901   ± 2706.717  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6111.139    ± 422.839  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6659.074    ± 140.226  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6471.511    ± 200.906  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        703.906     ± 48.273  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        550.365     ± 28.839  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5039.238    ± 811.505  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2977.842    ± 327.628  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4571.122     ± 37.672  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     488594.815   ± 4345.300  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     492305.098   ± 2539.424  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     497446.568   ± 2347.361  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     498135.255   ± 1622.798  ops/s
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
