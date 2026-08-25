# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-08-24T11:47:56Z
- **Commit:** [`ac0d68a`](https://github.com/Hawthorne001/client_java/commit/ac0d68a62886473ac4afd736602760e97024b528)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V45 96-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results for PR head

### CounterBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusNoLabelsInc | 65.61K | ± 805.59 | ops/s |
| codahaleIncNoLabels | 64.20K | ± 3.07K | ops/s |
| prometheusInc | 60.55K | ± 11.41K | ops/s |
| prometheusAdd | 55.86K | ± 488.73 | ops/s |
| openTelemetryIncNoLabels | 29.76K | ± 162.56 | ops/s |
| openTelemetryInc | 25.80K | ± 389.15 | ops/s |
| openTelemetryAdd | 22.16K | ± 278.52 | ops/s |
| simpleclientInc | 10.83K | ± 302.78 | ops/s |
| simpleclientNoLabelsInc | 10.73K | ± 413.67 | ops/s |
| simpleclientAdd | 10.25K | ± 253.30 | ops/s |

### HistogramBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusClassicPerThread | 15.26K | ± 202.24 | ops/s |
| simpleclient | 6.91K | ± 50.08 | ops/s |
| prometheusClassic | 5.81K | ± 463.96 | ops/s |
| prometheusNative | 5.20K | ± 569.34 | ops/s |
| prometheusClassicSingleThread | 4.47K | ± 64.70 | ops/s |
| openTelemetryClassic | 1.12K | ± 106.28 | ops/s |
| openTelemetryExponential | 1.02K | ± 52.83 | ops/s |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusWriteToNull | 33.22K | ± 442.03 | ops/s |
| openMetricsWriteToNull | 32.67K | ± 76.42 | ops/s |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusWriteToByteArray | 754.75K | ± 32.78K | ops/s |
| prometheusWriteToNull | 728.10K | ± 14.21K | ops/s |
| openMetricsWriteToByteArray | 679.19K | ± 12.28K | ops/s |
| openMetricsWriteToNull | 671.18K | ± 49.01K | ops/s |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      64199.175   ± 3065.879  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15      22162.706    ± 278.524  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15      25804.634    ± 389.154  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15      29756.344    ± 162.556  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      55861.908    ± 488.730  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      60550.911  ± 11409.965  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      65608.019    ± 805.593  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15      10245.185    ± 253.304  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15      10829.800    ± 302.776  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15      10730.959    ± 413.673  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15       1123.401    ± 106.282  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15       1020.338     ± 52.834  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5807.158    ± 463.955  ops/s
HistogramBenchmark.prometheusClassicPerThread       thrpt   15      15255.968    ± 202.244  ops/s
HistogramBenchmark.prometheusClassicSingleThread    thrpt   15       4471.048     ± 64.697  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       5203.164    ± 569.341  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       6910.983     ± 50.084  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      32665.060     ± 76.421  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      33219.068    ± 442.032  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     679187.221  ± 12276.425  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     671180.533  ± 49013.886  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     754752.010  ± 32782.098  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     728100.175  ± 14213.233  ops/s
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
