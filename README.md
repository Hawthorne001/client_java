# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-02-12T13:19:19Z
- **Commit:** [`e93cc0f`](https://github.com/Hawthorne001/client_java/commit/e93cc0fe1e3887124cf774acb78f5729ab7455a3)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.11.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.70K | ± 1.57K | ops/s | **fastest** |
| prometheusNoLabelsInc | 57.22K | ± 172.83 | ops/s | 1.1x slower |
| prometheusAdd | 51.72K | ± 104.61 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 49.48K | ± 1.28K | ops/s | 1.3x slower |
| simpleclientNoLabelsInc | 6.71K | ± 9.12 | ops/s | 9.8x slower |
| simpleclientInc | 6.54K | ± 236.14 | ops/s | 10x slower |
| simpleclientAdd | 6.27K | ± 161.00 | ops/s | 10x slower |
| openTelemetryAdd | 1.57K | ± 221.14 | ops/s | 42x slower |
| openTelemetryIncNoLabels | 1.30K | ± 103.86 | ops/s | 50x slower |
| openTelemetryInc | 1.23K | ± 29.08 | ops/s | 53x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 6.10K | ± 1.49K | ops/s | **fastest** |
| simpleclient | 4.56K | ± 14.81 | ops/s | 1.3x slower |
| prometheusNative | 2.87K | ± 315.51 | ops/s | 2.1x slower |
| openTelemetryClassic | 668.62 | ± 6.10 | ops/s | 9.1x slower |
| openTelemetryExponential | 554.74 | ± 12.94 | ops/s | 11x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 494.35K | ± 2.90K | ops/s | **fastest** |
| prometheusWriteToByteArray | 483.96K | ± 3.13K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 480.19K | ± 3.99K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 473.60K | ± 3.55K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49479.343   ± 1275.484  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1567.437    ± 221.135  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1230.031     ± 29.082  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1303.134    ± 103.860  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51722.860    ± 104.609  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65700.863   ± 1569.220  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      57215.411    ± 172.834  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6265.838    ± 160.997  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6537.367    ± 236.142  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6713.855      ± 9.123  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        668.618      ± 6.102  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        554.744     ± 12.937  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6104.558   ± 1485.345  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2870.170    ± 315.506  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4561.949     ± 14.813  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     480193.283   ± 3992.123  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     473598.145   ± 3549.452  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     483958.552   ± 3133.613  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     494346.670   ± 2895.930  ops/s
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
