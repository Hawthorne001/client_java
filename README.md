# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-05-07T13:00:11Z
- **Commit:** [`b5137b2`](https://github.com/Hawthorne001/client_java/commit/b5137b283a03b11f05a6979f4480593bda44b1b4)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1010-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 66.21K | ± 305.89 | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.93K | ± 483.75 | ops/s | 1.2x slower |
| prometheusAdd | 51.54K | ± 254.55 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 47.55K | ± 392.48 | ops/s | 1.4x slower |
| simpleclientInc | 6.69K | ± 20.89 | ops/s | 9.9x slower |
| simpleclientNoLabelsInc | 6.48K | ± 174.80 | ops/s | 10x slower |
| simpleclientAdd | 6.18K | ± 254.05 | ops/s | 11x slower |
| openTelemetryIncNoLabels | 3.36K | ± 122.79 | ops/s | 20x slower |
| openTelemetryInc | 3.32K | ± 454.28 | ops/s | 20x slower |
| openTelemetryAdd | 3.16K | ± 300.65 | ops/s | 21x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| simpleclient | 4.29K | ± 115.17 | ops/s | **fastest** |
| prometheusClassic | 4.15K | ± 444.88 | ops/s | 1.0x slower |
| prometheusNative | 2.84K | ± 283.90 | ops/s | 1.5x slower |
| openTelemetryClassic | 750.39 | ± 14.67 | ops/s | 5.7x slower |
| openTelemetryExponential | 638.34 | ± 67.63 | ops/s | 6.7x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 486.86K | ± 4.79K | ops/s | **fastest** |
| openMetricsWriteToNull | 483.69K | ± 2.99K | ops/s | 1.0x slower |
| prometheusWriteToByteArray | 483.68K | ± 3.20K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 469.27K | ± 3.79K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      47549.853    ± 392.484  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       3157.889    ± 300.649  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       3323.325    ± 454.283  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       3363.011    ± 122.794  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51544.715    ± 254.554  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      66207.020    ± 305.894  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56931.253    ± 483.754  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6180.124    ± 254.053  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6690.939     ± 20.887  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6475.351    ± 174.801  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        750.390     ± 14.674  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        638.344     ± 67.627  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       4151.444    ± 444.882  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2838.072    ± 283.901  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4289.576    ± 115.171  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     469271.387   ± 3792.798  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     483687.325   ± 2991.668  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     483675.394   ± 3200.228  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     486861.217   ± 4788.601  ops/s
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
