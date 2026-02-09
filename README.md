# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-02-09T11:30:46Z
- **Commit:** [`5cfa5c0`](https://github.com/Hawthorne001/client_java/commit/5cfa5c08cf169dc5854b16d5fb457e37dc7885a3)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.11.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 64.55K | ± 942.21 | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.45K | ± 1.36K | ops/s | 1.1x slower |
| prometheusAdd | 51.34K | ± 275.17 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 49.59K | ± 1.46K | ops/s | 1.3x slower |
| simpleclientInc | 6.78K | ± 19.74 | ops/s | 9.5x slower |
| simpleclientNoLabelsInc | 6.57K | ± 214.92 | ops/s | 9.8x slower |
| simpleclientAdd | 6.24K | ± 268.80 | ops/s | 10x slower |
| openTelemetryInc | 1.32K | ± 213.03 | ops/s | 49x slower |
| openTelemetryIncNoLabels | 1.32K | ± 155.32 | ops/s | 49x slower |
| openTelemetryAdd | 1.31K | ± 65.16 | ops/s | 49x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.64K | ± 1.91K | ops/s | **fastest** |
| simpleclient | 4.58K | ± 21.50 | ops/s | 1.2x slower |
| prometheusNative | 3.18K | ± 120.28 | ops/s | 1.8x slower |
| openTelemetryClassic | 657.72 | ± 17.19 | ops/s | 8.6x slower |
| openTelemetryExponential | 558.21 | ± 46.01 | ops/s | 10x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 491.76K | ± 2.73K | ops/s | **fastest** |
| prometheusWriteToByteArray | 488.16K | ± 4.19K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 476.15K | ± 4.12K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 472.50K | ± 1.76K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49591.439   ± 1464.770  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1306.033     ± 65.161  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1324.759    ± 213.027  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1316.635    ± 155.323  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51337.320    ± 275.172  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      64549.452    ± 942.213  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56450.757   ± 1359.841  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6243.398    ± 268.802  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6784.628     ± 19.737  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6574.499    ± 214.924  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        657.718     ± 17.189  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        558.208     ± 46.009  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5636.914   ± 1914.457  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3180.435    ± 120.282  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4575.972     ± 21.497  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     472504.863   ± 1760.130  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     476153.823   ± 4123.979  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     488157.247   ± 4185.602  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     491760.345   ± 2734.430  ops/s
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
