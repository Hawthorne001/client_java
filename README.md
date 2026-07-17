# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-07-16T11:51:24Z
- **Commit:** [`be2bc20`](https://github.com/Hawthorne001/client_java/commit/be2bc20fdf941be85a0ad020f5f405af623a7883)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1018-azure

## Results for PR head

### CounterBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusInc | 66.71K | ± 297.30 | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.28K | ± 1.13K | ops/s | 1.2x slower |
| codahaleIncNoLabels | 50.85K | ± 500.25 | ops/s | 1.3x slower |
| prometheusAdd | 50.19K | ± 1.02K | ops/s | 1.3x slower |
| simpleclientInc | 6.62K | ± 66.56 | ops/s | 10x slower |
| simpleclientAdd | 6.43K | ± 35.11 | ops/s | 10x slower |
| simpleclientNoLabelsInc | 6.34K | ± 9.97 | ops/s | 11x slower |
| openTelemetryIncNoLabels | 3.92K | ± 732.35 | ops/s | 17x slower |
| openTelemetryAdd | 3.43K | ± 187.81 | ops/s | 19x slower |
| openTelemetryInc | 3.05K | ± 134.29 | ops/s | 22x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusClassic | 6.91K | ± 2.22K | ops/s | **fastest** |
| simpleclient | 4.42K | ± 66.98 | ops/s | 1.6x slower |
| prometheusNative | 3.08K | ± 170.03 | ops/s | 2.2x slower |
| openTelemetryClassic | 745.54 | ± 27.17 | ops/s | 9.3x slower |
| openTelemetryExponential | 581.36 | ± 28.64 | ops/s | 12x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusWriteToNull | 23.72K | ± 844.11 | ops/s | **fastest** |
| openMetricsWriteToNull | 23.08K | ± 1.26K | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusWriteToNull | 516.90K | ± 4.14K | ops/s | **fastest** |
| prometheusWriteToByteArray | 509.02K | ± 4.65K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 496.04K | ± 6.73K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 488.74K | ± 6.47K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      50852.741    ± 500.246  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       3434.109    ± 187.812  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       3052.543    ± 134.288  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       3923.516    ± 732.350  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      50189.521   ± 1024.243  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      66710.527    ± 297.303  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56280.548   ± 1132.306  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6433.514     ± 35.112  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6617.566     ± 66.559  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6335.444      ± 9.966  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        745.544     ± 27.171  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        581.359     ± 28.640  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6914.390   ± 2217.703  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3076.225    ± 170.026  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4418.156     ± 66.979  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      23078.322   ± 1263.811  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      23720.405    ± 844.110  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     488744.926   ± 6467.303  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     496036.042   ± 6732.534  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     509018.765   ± 4652.400  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     516898.434   ± 4138.156  ops/s
```

## Notes

- **Score** = Throughput in operations per second (higher is better)
- **Error** = 99.9% confidence interval
- **Within run** compares benchmarks in the same result set, not against the base commit.

## Benchmark Descriptions

| Benchmark | Description |
|:----------|:------------|
| **CounterBenchmark** | Counter increment performance: Prometheus, OpenTelemetry, simpleclient, Codahale |
| **HistogramBenchmark** | Histogram observation performance (classic vs native/exponential) |
| **TextFormatUtilBenchmark** | Metric exposition format writing speed |
