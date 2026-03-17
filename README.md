# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-03-17T08:37:25Z
- **Commit:** [`b81332e`](https://github.com/Hawthorne001/client_java/commit/b81332e3a09e465f956f118a2403e64b83771ae5)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.14.0-1017-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 66.65K | ± 705.26 | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.50K | ± 1.01K | ops/s | 1.2x slower |
| prometheusAdd | 51.45K | ± 220.01 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.18K | ± 2.80K | ops/s | 1.4x slower |
| simpleclientInc | 6.67K | ± 159.47 | ops/s | 10.0x slower |
| simpleclientNoLabelsInc | 6.56K | ± 205.88 | ops/s | 10x slower |
| simpleclientAdd | 6.31K | ± 190.40 | ops/s | 11x slower |
| openTelemetryAdd | 1.39K | ± 214.34 | ops/s | 48x slower |
| openTelemetryInc | 1.31K | ± 28.20 | ops/s | 51x slower |
| openTelemetryIncNoLabels | 1.27K | ± 16.54 | ops/s | 53x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.30K | ± 1.44K | ops/s | **fastest** |
| simpleclient | 4.50K | ± 54.61 | ops/s | 1.2x slower |
| prometheusNative | 2.99K | ± 284.74 | ops/s | 1.8x slower |
| openTelemetryClassic | 707.22 | ± 45.12 | ops/s | 7.5x slower |
| openTelemetryExponential | 583.30 | ± 36.95 | ops/s | 9.1x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 478.22K | ± 6.04K | ops/s | **fastest** |
| prometheusWriteToByteArray | 475.39K | ± 4.38K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 470.62K | ± 4.09K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 461.47K | ± 3.02K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48179.419   ± 2802.906  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1392.939    ± 214.343  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1305.939     ± 28.196  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1268.772     ± 16.537  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51454.661    ± 220.008  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      66653.362    ± 705.264  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56496.540   ± 1012.221  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6314.316    ± 190.402  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6673.053    ± 159.467  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6563.167    ± 205.878  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        707.222     ± 45.117  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        583.300     ± 36.946  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5296.885   ± 1437.115  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2991.139    ± 284.741  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4501.729     ± 54.609  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     461470.483   ± 3019.074  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     470622.754   ± 4089.115  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     475392.018   ± 4384.226  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     478222.461   ± 6038.973  ops/s
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
