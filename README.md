# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-04-06T16:09:51Z
- **Commit:** [`0fa1ad7`](https://github.com/Hawthorne001/client_java/commit/0fa1ad7dcb71f7f02e19ee9604c07d9c48802f04)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1008-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.92K | ± 1.83K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.01K | ± 1.26K | ops/s | 1.2x slower |
| prometheusAdd | 51.15K | ± 151.10 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 49.74K | ± 1.62K | ops/s | 1.3x slower |
| simpleclientNoLabelsInc | 6.63K | ± 20.12 | ops/s | 9.9x slower |
| simpleclientInc | 6.58K | ± 184.56 | ops/s | 10x slower |
| simpleclientAdd | 6.13K | ± 302.15 | ops/s | 11x slower |
| openTelemetryIncNoLabels | 1.36K | ± 246.08 | ops/s | 49x slower |
| openTelemetryAdd | 1.30K | ± 108.39 | ops/s | 51x slower |
| openTelemetryInc | 1.27K | ± 44.53 | ops/s | 52x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 6.33K | ± 857.24 | ops/s | **fastest** |
| simpleclient | 4.46K | ± 51.36 | ops/s | 1.4x slower |
| prometheusNative | 3.18K | ± 100.87 | ops/s | 2.0x slower |
| openTelemetryClassic | 700.48 | ± 8.21 | ops/s | 9.0x slower |
| openTelemetryExponential | 514.15 | ± 10.22 | ops/s | 12x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 485.02K | ± 4.45K | ops/s | **fastest** |
| prometheusWriteToByteArray | 481.31K | ± 3.80K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 475.75K | ± 10.57K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 470.55K | ± 3.93K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49744.326   ± 1618.889  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1296.380    ± 108.386  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1273.854     ± 44.526  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1357.368    ± 246.076  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51145.546    ± 151.097  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65917.412   ± 1833.828  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56013.561   ± 1260.828  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6126.908    ± 302.149  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6578.680    ± 184.556  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6625.308     ± 20.125  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        700.480      ± 8.205  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        514.145     ± 10.220  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6329.583    ± 857.241  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3184.645    ± 100.865  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4459.959     ± 51.356  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     470546.800   ± 3932.651  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     475753.847  ± 10569.661  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     481313.250   ± 3795.366  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     485016.056   ± 4453.339  ops/s
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
