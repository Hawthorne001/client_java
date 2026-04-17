# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-04-17T23:36:31Z
- **Commit:** [`4b69f40`](https://github.com/Hawthorne001/client_java/commit/4b69f40bd4e616d69468ce99dc4323162287a577)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1010-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 60.42K | ± 795.94 | ops/s | **fastest** |
| prometheusNoLabelsInc | 50.88K | ± 995.50 | ops/s | 1.2x slower |
| prometheusAdd | 48.78K | ± 764.11 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 44.07K | ± 146.81 | ops/s | 1.4x slower |
| simpleclientInc | 6.18K | ± 214.91 | ops/s | 9.8x slower |
| simpleclientAdd | 5.90K | ± 243.94 | ops/s | 10x slower |
| simpleclientNoLabelsInc | 5.82K | ± 70.73 | ops/s | 10x slower |
| openTelemetryInc | 1.40K | ± 50.22 | ops/s | 43x slower |
| openTelemetryAdd | 1.40K | ± 61.23 | ops/s | 43x slower |
| openTelemetryIncNoLabels | 1.32K | ± 114.24 | ops/s | 46x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.13K | ± 1.87K | ops/s | **fastest** |
| simpleclient | 4.39K | ± 46.98 | ops/s | 1.2x slower |
| prometheusNative | 2.91K | ± 160.16 | ops/s | 1.8x slower |
| openTelemetryClassic | 636.88 | ± 41.31 | ops/s | 8.1x slower |
| openTelemetryExponential | 539.15 | ± 17.83 | ops/s | 9.5x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 565.63K | ± 2.27K | ops/s | **fastest** |
| prometheusWriteToByteArray | 547.60K | ± 6.64K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 546.26K | ± 1.22K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 527.08K | ± 2.98K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      44072.779    ± 146.813  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1404.204     ± 61.231  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1404.444     ± 50.216  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1315.233    ± 114.243  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      48779.471    ± 764.109  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      60424.876    ± 795.943  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      50883.745    ± 995.502  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       5895.218    ± 243.940  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6177.141    ± 214.913  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       5817.411     ± 70.730  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        636.884     ± 41.308  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        539.154     ± 17.833  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5131.417   ± 1871.240  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2905.022    ± 160.157  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4387.040     ± 46.984  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     527076.240   ± 2983.353  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     546262.095   ± 1223.552  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     547601.765   ± 6637.152  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     565626.668   ± 2273.231  ops/s
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
