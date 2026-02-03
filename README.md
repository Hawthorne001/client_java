# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-02-03T07:10:22Z
- **Commit:** [`c1adde1`](https://github.com/Hawthorne001/client_java/commit/c1adde10a7ee27a48e4a45a6be6e29ed0d096dcf)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.11.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.23K | ± 1.08K | ops/s | **fastest** |
| prometheusNoLabelsInc | 57.11K | ± 376.73 | ops/s | 1.1x slower |
| prometheusAdd | 51.29K | ± 571.58 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 49.37K | ± 1.64K | ops/s | 1.3x slower |
| simpleclientInc | 6.71K | ± 98.46 | ops/s | 9.7x slower |
| simpleclientNoLabelsInc | 6.58K | ± 116.40 | ops/s | 9.9x slower |
| simpleclientAdd | 6.02K | ± 227.65 | ops/s | 11x slower |
| openTelemetryAdd | 1.45K | ± 159.15 | ops/s | 45x slower |
| openTelemetryIncNoLabels | 1.22K | ± 16.65 | ops/s | 53x slower |
| openTelemetryInc | 1.21K | ± 28.05 | ops/s | 54x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.11K | ± 70.90 | ops/s | **fastest** |
| simpleclient | 4.50K | ± 25.42 | ops/s | 1.1x slower |
| prometheusNative | 3.09K | ± 148.83 | ops/s | 1.7x slower |
| openTelemetryClassic | 678.10 | ± 22.06 | ops/s | 7.5x slower |
| openTelemetryExponential | 530.33 | ± 12.00 | ops/s | 9.6x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 534.29K | ± 3.46K | ops/s | **fastest** |
| prometheusWriteToByteArray | 519.94K | ± 8.74K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 507.73K | ± 3.22K | ops/s | 1.1x slower |
| openMetricsWriteToNull | 497.82K | ± 11.52K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49369.701   ± 1637.745  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1454.450    ± 159.154  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1208.029     ± 28.047  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1222.150     ± 16.655  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51291.376    ± 571.577  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65229.031   ± 1080.605  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      57111.090    ± 376.730  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6022.350    ± 227.654  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6709.478     ± 98.457  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6581.549    ± 116.399  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        678.096     ± 22.063  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        530.334     ± 12.004  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5107.513     ± 70.904  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3092.445    ± 148.829  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4496.120     ± 25.425  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     507727.602   ± 3215.552  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     497822.882  ± 11524.954  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     519944.632   ± 8744.034  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     534290.861   ± 3463.179  ops/s
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
