# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-04-07T16:53:14Z
- **Commit:** [`0fa1ad7`](https://github.com/Hawthorne001/client_java/commit/0fa1ad7dcb71f7f02e19ee9604c07d9c48802f04)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1008-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 64.31K | ± 1.32K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.44K | ± 1.09K | ops/s | 1.1x slower |
| prometheusAdd | 51.29K | ± 236.02 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 47.90K | ± 551.09 | ops/s | 1.3x slower |
| simpleclientInc | 6.67K | ± 67.29 | ops/s | 9.6x slower |
| simpleclientNoLabelsInc | 6.38K | ± 226.32 | ops/s | 10x slower |
| simpleclientAdd | 6.20K | ± 196.28 | ops/s | 10x slower |
| openTelemetryIncNoLabels | 1.34K | ± 41.24 | ops/s | 48x slower |
| openTelemetryAdd | 1.28K | ± 78.26 | ops/s | 50x slower |
| openTelemetryInc | 1.24K | ± 88.70 | ops/s | 52x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 6.94K | ± 2.48K | ops/s | **fastest** |
| simpleclient | 4.41K | ± 16.16 | ops/s | 1.6x slower |
| prometheusNative | 2.98K | ± 290.98 | ops/s | 2.3x slower |
| openTelemetryClassic | 696.63 | ± 38.94 | ops/s | 10.0x slower |
| openTelemetryExponential | 565.12 | ± 26.61 | ops/s | 12x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 493.82K | ± 4.44K | ops/s | **fastest** |
| prometheusWriteToByteArray | 488.90K | ± 1.95K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 483.60K | ± 2.55K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 475.18K | ± 3.84K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      47897.750    ± 551.091  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1279.639     ± 78.259  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1235.933     ± 88.695  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1339.201     ± 41.240  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51294.166    ± 236.022  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      64307.223   ± 1318.514  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56443.138   ± 1094.384  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6203.848    ± 196.277  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6672.094     ± 67.286  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6376.999    ± 226.318  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        696.629     ± 38.937  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        565.121     ± 26.606  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6936.077   ± 2481.356  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2976.623    ± 290.978  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4410.763     ± 16.156  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     475178.638   ± 3838.777  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     483599.892   ± 2549.065  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     488895.285   ± 1954.765  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     493823.550   ± 4436.118  ops/s
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
