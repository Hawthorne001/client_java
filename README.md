# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-07-18T12:54:12Z
- **Commit:** [`8d91443`](https://github.com/Hawthorne001/client_java/commit/8d91443665952d8a2585a9e2f220a5811ef2a051)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1020-azure

## Results for PR head

### CounterBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusInc | 60.20K | ± 1.01K | ops/s | **fastest** |
| prometheusNoLabelsInc | 51.44K | ± 583.86 | ops/s | 1.2x slower |
| prometheusAdd | 47.94K | ± 498.32 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 44.22K | ± 181.32 | ops/s | 1.4x slower |
| simpleclientInc | 6.23K | ± 74.20 | ops/s | 9.7x slower |
| simpleclientAdd | 6.02K | ± 136.07 | ops/s | 10.0x slower |
| simpleclientNoLabelsInc | 5.90K | ± 31.45 | ops/s | 10x slower |
| openTelemetryIncNoLabels | 5.56K | ± 1.39K | ops/s | 11x slower |
| openTelemetryInc | 4.44K | ± 1.39K | ops/s | 14x slower |
| openTelemetryAdd | 3.36K | ± 202.52 | ops/s | 18x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusClassic | 6.81K | ± 861.13 | ops/s | **fastest** |
| simpleclient | 4.39K | ± 28.59 | ops/s | 1.6x slower |
| prometheusNative | 2.76K | ± 145.08 | ops/s | 2.5x slower |
| openTelemetryClassic | 721.23 | ± 16.68 | ops/s | 9.4x slower |
| openTelemetryExponential | 573.43 | ± 29.56 | ops/s | 12x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusWriteToNull | 27.55K | ± 160.07 | ops/s | **fastest** |
| openMetricsWriteToNull | 27.31K | ± 171.24 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusWriteToNull | 571.31K | ± 19.16K | ops/s | **fastest** |
| prometheusWriteToByteArray | 567.40K | ± 11.96K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 548.28K | ± 14.37K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 536.52K | ± 6.22K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      44221.123    ± 181.320  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       3360.729    ± 202.517  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       4438.659   ± 1387.234  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       5563.609   ± 1388.195  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      47935.269    ± 498.318  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      60197.756   ± 1014.957  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      51443.621    ± 583.865  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6020.560    ± 136.075  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6233.787     ± 74.202  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       5903.294     ± 31.449  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        721.230     ± 16.684  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        573.430     ± 29.560  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6810.240    ± 861.127  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2763.316    ± 145.076  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4393.688     ± 28.592  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      27311.261    ± 171.240  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      27551.592    ± 160.068  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     536518.326   ± 6222.338  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     548279.769  ± 14369.792  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     567400.799  ± 11964.847  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     571314.014  ± 19157.418  ops/s
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
