# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-08-16T10:32:14Z
- **Commit:** [`90f99d6`](https://github.com/Hawthorne001/client_java/commit/90f99d635109472d8ccca304f044f93a1b0f1436)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results for PR head

### CounterBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusInc | 75.74K | ± 1.49K | ops/s | **fastest** |
| prometheusNoLabelsInc | 66.13K | ± 894.27 | ops/s | 1.1x slower |
| prometheusAdd | 59.70K | ± 5.83K | ops/s | 1.3x slower |
| codahaleIncNoLabels | 56.02K | ± 1.41K | ops/s | 1.4x slower |
| openTelemetryIncNoLabels | 22.13K | ± 87.89 | ops/s | 3.4x slower |
| openTelemetryInc | 17.66K | ± 336.33 | ops/s | 4.3x slower |
| openTelemetryAdd | 15.70K | ± 124.29 | ops/s | 4.8x slower |
| simpleclientInc | 7.97K | ± 124.07 | ops/s | 9.5x slower |
| simpleclientNoLabelsInc | 7.67K | ± 6.59 | ops/s | 9.9x slower |
| simpleclientAdd | 7.55K | ± 442.56 | ops/s | 10x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusClassicPerThread | 17.63K | ± 124.07 | ops/s | **fastest** |
| prometheusClassicSingleThread | 7.48K | ± 19.02 | ops/s | 2.4x slower |
| prometheusClassic | 7.22K | ± 1.59K | ops/s | 2.4x slower |
| simpleclient | 5.82K | ± 162.46 | ops/s | 3.0x slower |
| prometheusNative | 3.89K | ± 394.63 | ops/s | 4.5x slower |
| openTelemetryClassic | 1.11K | ± 46.88 | ops/s | 16x slower |
| openTelemetryExponential | 863.45 | ± 57.02 | ops/s | 20x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusWriteToNull | 35.50K | ± 225.90 | ops/s | **fastest** |
| openMetricsWriteToNull | 35.42K | ± 212.90 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusWriteToNull | 706.61K | ± 8.02K | ops/s | **fastest** |
| prometheusWriteToByteArray | 690.27K | ± 3.44K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 661.34K | ± 3.98K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 645.84K | ± 4.57K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      56022.824   ± 1407.214  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15      15703.015    ± 124.286  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15      17655.341    ± 336.330  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15      22134.582     ± 87.893  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      59697.558   ± 5833.938  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      75744.376   ± 1490.281  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      66131.147    ± 894.271  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       7554.253    ± 442.562  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       7971.896    ± 124.073  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       7667.931      ± 6.588  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15       1108.590     ± 46.884  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        863.454     ± 57.023  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       7222.306   ± 1591.330  ops/s
HistogramBenchmark.prometheusClassicPerThread       thrpt   15      17630.885    ± 124.069  ops/s
HistogramBenchmark.prometheusClassicSingleThread    thrpt   15       7484.265     ± 19.019  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3887.824    ± 394.626  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       5823.979    ± 162.462  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      35416.041    ± 212.896  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      35499.976    ± 225.897  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     645835.034   ± 4571.401  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     661344.387   ± 3978.303  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     690272.989   ± 3441.777  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     706610.178   ± 8018.467  ops/s
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
