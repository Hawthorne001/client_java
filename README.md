# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-03-06T01:28:10Z
- **Commit:** [`b9906c1`](https://github.com/Hawthorne001/client_java/commit/b9906c11d6b9125b642ffbe6527dfe727880090b)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.14.0-1017-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 66.12K | ± 883.67 | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.45K | ± 1.42K | ops/s | 1.2x slower |
| prometheusAdd | 51.38K | ± 111.61 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.72K | ± 1.36K | ops/s | 1.4x slower |
| simpleclientInc | 6.67K | ± 149.58 | ops/s | 9.9x slower |
| simpleclientNoLabelsInc | 6.61K | ± 135.42 | ops/s | 10.0x slower |
| simpleclientAdd | 6.30K | ± 211.24 | ops/s | 11x slower |
| openTelemetryAdd | 1.41K | ± 230.07 | ops/s | 47x slower |
| openTelemetryInc | 1.25K | ± 23.84 | ops/s | 53x slower |
| openTelemetryIncNoLabels | 1.21K | ± 9.33 | ops/s | 54x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.45K | ± 1.41K | ops/s | **fastest** |
| simpleclient | 4.55K | ± 36.00 | ops/s | 1.2x slower |
| prometheusNative | 3.05K | ± 293.81 | ops/s | 1.8x slower |
| openTelemetryClassic | 690.18 | ± 7.90 | ops/s | 7.9x slower |
| openTelemetryExponential | 558.49 | ± 56.26 | ops/s | 9.8x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 489.76K | ± 4.98K | ops/s | **fastest** |
| openMetricsWriteToNull | 483.76K | ± 3.80K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 480.45K | ± 7.74K | ops/s | 1.0x slower |
| prometheusWriteToByteArray | 480.23K | ± 3.98K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48722.446   ± 1363.088  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1407.124    ± 230.074  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1250.013     ± 23.844  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1213.554      ± 9.329  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51383.497    ± 111.610  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      66122.334    ± 883.670  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56448.022   ± 1417.218  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6296.873    ± 211.239  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6673.355    ± 149.579  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6613.491    ± 135.423  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        690.179      ± 7.903  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        558.486     ± 56.259  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5446.171   ± 1414.282  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3049.575    ± 293.814  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4548.798     ± 36.000  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     480446.101   ± 7741.957  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     483758.225   ± 3795.217  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     480234.501   ± 3983.612  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     489762.143   ± 4978.742  ops/s
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
