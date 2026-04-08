# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-04-08T17:43:54Z
- **Commit:** [`0fa1ad7`](https://github.com/Hawthorne001/client_java/commit/0fa1ad7dcb71f7f02e19ee9604c07d9c48802f04)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1008-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 66.88K | ± 349.49 | ops/s | **fastest** |
| prometheusNoLabelsInc | 55.43K | ± 1.34K | ops/s | 1.2x slower |
| prometheusAdd | 51.38K | ± 261.21 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 50.48K | ± 471.60 | ops/s | 1.3x slower |
| simpleclientInc | 6.51K | ± 180.29 | ops/s | 10x slower |
| simpleclientNoLabelsInc | 6.41K | ± 167.45 | ops/s | 10x slower |
| simpleclientAdd | 5.92K | ± 158.55 | ops/s | 11x slower |
| openTelemetryAdd | 1.61K | ± 312.40 | ops/s | 42x slower |
| openTelemetryInc | 1.23K | ± 33.29 | ops/s | 55x slower |
| openTelemetryIncNoLabels | 1.20K | ± 30.90 | ops/s | 56x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.19K | ± 913.13 | ops/s | **fastest** |
| simpleclient | 4.44K | ± 67.17 | ops/s | 1.2x slower |
| prometheusNative | 2.94K | ± 236.80 | ops/s | 1.8x slower |
| openTelemetryClassic | 701.28 | ± 28.21 | ops/s | 7.4x slower |
| openTelemetryExponential | 554.66 | ± 15.27 | ops/s | 9.3x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 489.16K | ± 4.41K | ops/s | **fastest** |
| prometheusWriteToByteArray | 485.55K | ± 4.54K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 481.36K | ± 2.27K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 474.93K | ± 8.01K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      50478.543    ± 471.604  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1607.073    ± 312.396  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1225.306     ± 33.294  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1199.841     ± 30.900  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51381.113    ± 261.205  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      66878.642    ± 349.487  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      55429.023   ± 1335.643  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       5916.450    ± 158.554  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6510.628    ± 180.293  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6408.375    ± 167.454  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        701.278     ± 28.212  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        554.661     ± 15.275  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5185.244    ± 913.127  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2939.380    ± 236.797  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4438.482     ± 67.169  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     474932.891   ± 8011.790  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     481360.170   ± 2274.328  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     485554.792   ± 4544.069  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     489157.908   ± 4406.316  ops/s
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
