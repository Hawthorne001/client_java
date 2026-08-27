# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-08-26T12:54:32Z
- **Commit:** [`6f88666`](https://github.com/Hawthorne001/client_java/commit/6f8866650d5ae4a7fe5500556f149ed9f9fd234d)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results for PR head

### CounterBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusInc | 59.70K | ± 1.47K | ops/s |
| prometheusNoLabelsInc | 51.79K | ± 833.41 | ops/s |
| prometheusAdd | 48.94K | ± 1.55K | ops/s |
| codahaleIncNoLabels | 44.60K | ± 1.84K | ops/s |
| openTelemetryIncNoLabels | 17.03K | ± 210.63 | ops/s |
| openTelemetryInc | 14.11K | ± 311.86 | ops/s |
| openTelemetryAdd | 11.42K | ± 1.30K | ops/s |
| simpleclientInc | 6.09K | ± 23.39 | ops/s |
| simpleclientNoLabelsInc | 5.91K | ± 21.63 | ops/s |
| simpleclientAdd | 5.88K | ± 311.50 | ops/s |

### HistogramBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusClassicPerThread | 13.94K | ± 84.37 | ops/s |
| prometheusClassic | 6.39K | ± 1.45K | ops/s |
| prometheusClassicSingleThread | 5.80K | ± 25.05 | ops/s |
| simpleclient | 4.51K | ± 66.58 | ops/s |
| prometheusNative | 3.01K | ± 102.24 | ops/s |
| openTelemetryClassic | 750.67 | ± 29.25 | ops/s |
| openTelemetryExponential | 672.17 | ± 18.35 | ops/s |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusWriteToNull | 27.42K | ± 409.75 | ops/s |
| openMetricsWriteToNull | 27.05K | ± 502.86 | ops/s |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusWriteToNull | 575.29K | ± 4.68K | ops/s |
| prometheusWriteToByteArray | 565.35K | ± 3.48K | ops/s |
| openMetricsWriteToNull | 543.16K | ± 4.76K | ops/s |
| openMetricsWriteToByteArray | 534.97K | ± 4.41K | ops/s |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      44597.394   ± 1838.699  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15      11424.524   ± 1298.201  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15      14112.975    ± 311.862  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15      17034.168    ± 210.633  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      48936.215   ± 1552.075  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      59701.123   ± 1469.385  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      51792.900    ± 833.409  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       5880.364    ± 311.497  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6094.481     ± 23.388  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       5912.524     ± 21.630  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        750.670     ± 29.253  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        672.167     ± 18.352  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6388.659   ± 1449.206  ops/s
HistogramBenchmark.prometheusClassicPerThread       thrpt   15      13935.507     ± 84.366  ops/s
HistogramBenchmark.prometheusClassicSingleThread    thrpt   15       5796.190     ± 25.048  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3008.196    ± 102.243  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4514.987     ± 66.576  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      27049.817    ± 502.864  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      27417.536    ± 409.745  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     534969.461   ± 4411.206  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     543160.663   ± 4760.710  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     565351.271   ± 3479.624  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     575294.950   ± 4682.050  ops/s
```

## Notes

- **Score** = the JMH primary metric; throughput is higher-is-better and latency is lower-is-better.
- **Error** = 99.9% confidence interval
- Scores for different benchmark methods are not ranked against one another; they may measure different workloads.

## Benchmark Descriptions

| Benchmark | Description |
|:----------|:------------|
| **CounterBenchmark** | Counter increment performance: Prometheus, OpenTelemetry, simpleclient, Codahale |
| **HistogramBenchmark** | Histogram observation performance (classic vs native/exponential) |
| **TextFormatUtilBenchmark** | Metric exposition format writing speed |
