# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-02-26T18:53:15Z
- **Commit:** [`fc21983`](https://github.com/Hawthorne001/client_java/commit/fc219837f90c194962b33dadab179f19738d75b3)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.14.0-1017-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 63.38K | ± 5.24K | ops/s | **fastest** |
| prometheusNoLabelsInc | 55.27K | ± 2.57K | ops/s | 1.1x slower |
| prometheusAdd | 51.57K | ± 207.28 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 48.18K | ± 303.97 | ops/s | 1.3x slower |
| simpleclientInc | 6.75K | ± 18.01 | ops/s | 9.4x slower |
| simpleclientNoLabelsInc | 6.68K | ± 21.88 | ops/s | 9.5x slower |
| simpleclientAdd | 6.19K | ± 209.99 | ops/s | 10x slower |
| openTelemetryAdd | 1.44K | ± 281.21 | ops/s | 44x slower |
| openTelemetryIncNoLabels | 1.43K | ± 164.27 | ops/s | 44x slower |
| openTelemetryInc | 1.28K | ± 22.61 | ops/s | 49x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 7.19K | ± 87.23 | ops/s | **fastest** |
| simpleclient | 4.50K | ± 65.21 | ops/s | 1.6x slower |
| prometheusNative | 2.88K | ± 279.88 | ops/s | 2.5x slower |
| openTelemetryClassic | 645.84 | ± 18.55 | ops/s | 11x slower |
| openTelemetryExponential | 546.09 | ± 30.10 | ops/s | 13x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 498.83K | ± 2.69K | ops/s | **fastest** |
| prometheusWriteToByteArray | 494.26K | ± 3.20K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 489.30K | ± 3.31K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 485.87K | ± 3.56K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48179.315    ± 303.971  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1440.608    ± 281.205  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1280.498     ± 22.610  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1425.340    ± 164.272  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51566.182    ± 207.279  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      63378.602   ± 5240.165  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      55268.274   ± 2571.213  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6193.304    ± 209.988  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6748.863     ± 18.007  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6683.608     ± 21.875  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        645.837     ± 18.555  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        546.091     ± 30.099  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       7186.356     ± 87.234  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2880.131    ± 279.879  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4500.234     ± 65.207  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     485866.967   ± 3558.219  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     489301.034   ± 3309.045  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     494264.584   ± 3202.238  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     498826.255   ± 2692.468  ops/s
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
