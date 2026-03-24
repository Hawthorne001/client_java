# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-03-24T10:42:59Z
- **Commit:** [`6beb7fd`](https://github.com/Hawthorne001/client_java/commit/6beb7fd3f26fb1629aae21d9d85d975f63d1a6b8)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.14.0-1017-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 64.87K | ± 1.81K | ops/s | **fastest** |
| prometheusNoLabelsInc | 55.52K | ± 2.84K | ops/s | 1.2x slower |
| prometheusAdd | 51.50K | ± 253.08 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 50.57K | ± 669.98 | ops/s | 1.3x slower |
| simpleclientInc | 6.77K | ± 33.96 | ops/s | 9.6x slower |
| simpleclientNoLabelsInc | 6.56K | ± 203.94 | ops/s | 9.9x slower |
| simpleclientAdd | 6.33K | ± 314.72 | ops/s | 10x slower |
| openTelemetryAdd | 1.58K | ± 189.60 | ops/s | 41x slower |
| openTelemetryIncNoLabels | 1.23K | ± 39.57 | ops/s | 53x slower |
| openTelemetryInc | 1.21K | ± 48.18 | ops/s | 54x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 6.42K | ± 1.08K | ops/s | **fastest** |
| simpleclient | 4.55K | ± 21.07 | ops/s | 1.4x slower |
| prometheusNative | 2.61K | ± 94.52 | ops/s | 2.5x slower |
| openTelemetryClassic | 658.30 | ± 24.07 | ops/s | 9.8x slower |
| openTelemetryExponential | 545.32 | ± 7.36 | ops/s | 12x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 484.93K | ± 10.54K | ops/s | **fastest** |
| openMetricsWriteToNull | 484.20K | ± 4.84K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 478.58K | ± 2.55K | ops/s | 1.0x slower |
| prometheusWriteToByteArray | 474.05K | ± 12.04K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      50570.948    ± 669.979  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1576.142    ± 189.599  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1211.458     ± 48.176  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1228.619     ± 39.566  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51500.275    ± 253.080  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      64871.084   ± 1810.213  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      55518.981   ± 2840.098  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6330.478    ± 314.716  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6770.930     ± 33.958  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6561.477    ± 203.935  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        658.305     ± 24.068  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        545.315      ± 7.363  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6420.648   ± 1083.732  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2611.052     ± 94.520  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4545.516     ± 21.069  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     478575.145   ± 2550.097  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     484199.933   ± 4840.771  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     474053.318  ± 12035.758  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     484932.027  ± 10536.864  ops/s
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
