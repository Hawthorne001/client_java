# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-06-28T09:56:47Z
- **Commit:** [`2a2c73d`](https://github.com/Hawthorne001/client_java/commit/2a2c73d7d23bfa291b10df85056027398e8a868d)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.59K | ± 1.23K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.42K | ± 66.54 | ops/s | 1.2x slower |
| prometheusAdd | 51.38K | ± 195.72 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 47.53K | ± 492.39 | ops/s | 1.4x slower |
| simpleclientInc | 6.57K | ± 128.62 | ops/s | 10.0x slower |
| simpleclientAdd | 6.46K | ± 33.91 | ops/s | 10x slower |
| simpleclientNoLabelsInc | 6.34K | ± 10.32 | ops/s | 10x slower |
| openTelemetryIncNoLabels | 3.50K | ± 375.09 | ops/s | 19x slower |
| openTelemetryInc | 3.24K | ± 235.63 | ops/s | 20x slower |
| openTelemetryAdd | 2.93K | ± 171.20 | ops/s | 22x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 4.99K | ± 804.31 | ops/s | **fastest** |
| simpleclient | 4.35K | ± 10.50 | ops/s | 1.1x slower |
| prometheusNative | 2.54K | ± 102.51 | ops/s | 2.0x slower |
| openTelemetryClassic | 718.60 | ± 27.05 | ops/s | 6.9x slower |
| openTelemetryExponential | 546.02 | ± 26.20 | ops/s | 9.1x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| openMetricsWriteToNull | 23.57K | ± 286.55 | ops/s | **fastest** |
| prometheusWriteToNull | 23.52K | ± 348.77 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 510.45K | ± 4.57K | ops/s | **fastest** |
| prometheusWriteToByteArray | 503.62K | ± 3.43K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 486.94K | ± 1.98K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 485.04K | ± 4.34K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      47529.392    ± 492.387  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       2929.318    ± 171.196  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       3240.756    ± 235.628  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       3500.890    ± 375.091  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51384.694    ± 195.718  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65587.370   ± 1228.774  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56417.350     ± 66.540  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6459.231     ± 33.908  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6569.316    ± 128.625  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6343.386     ± 10.322  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        718.603     ± 27.050  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        546.023     ± 26.203  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       4991.390    ± 804.315  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2541.057    ± 102.510  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4354.884     ± 10.498  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      23566.685    ± 286.547  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      23521.832    ± 348.772  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     485036.445   ± 4337.463  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     486941.250   ± 1980.791  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     503616.529   ± 3430.217  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     510452.914   ± 4569.263  ops/s
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
