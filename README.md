# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-09-22T18:03:03Z
- **Commit:** [`c658f3d`](https://github.com/Hawthorne001/client_java/commit/c658f3da2d8c6f5e90837dcd3681b744242d796d)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 1/4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results for PR head

### CounterBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusCachedLabelValuesInc | 556.55M | ± 5657.24K | ops/s |
| prometheusCachedLabelValuesIncSingleThread | 334.65M | ± 506.32K | ops/s |
| prometheusLabelValuesInc | 119.30M | ± 1053.42K | ops/s |
| prometheusLabelValuesIncSingleThread | 58.53M | ± 179.71K | ops/s |
| prometheusInc | 65.00K | ± 1.33K | ops/s |
| prometheusNoLabelsInc | 56.82K | ± 331.09 | ops/s |
| prometheusAdd | 51.42K | ± 158.39 | ops/s |
| codahaleIncNoLabels | 49.46K | ± 1.08K | ops/s |
| openTelemetryBoundInc | 37.84K | ± 403.84 | ops/s |
| openTelemetryBoundAdd | 31.84K | ± 182.36 | ops/s |
| openTelemetryIncNoLabels | 22.71K | ± 1.16K | ops/s |
| openTelemetryInc | 18.00K | ± 266.30 | ops/s |
| openTelemetryAdd | 15.57K | ± 41.09 | ops/s |
| simpleclientInc | 6.58K | ± 13.31 | ops/s |
| simpleclientAdd | 6.44K | ± 29.64 | ops/s |
| simpleclientNoLabelsInc | 6.33K | ± 14.93 | ops/s |

### HistogramBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusClassicPerThread | 12.06K | ± 18.96 | ops/s |
| prometheusClassic | 6.30K | ± 1.00K | ops/s |
| openTelemetryBoundClassic | 5.34K | ± 1.90K | ops/s |
| prometheusClassicSingleThread | 4.54K | ± 17.59 | ops/s |
| simpleclient | 4.43K | ± 13.25 | ops/s |
| openTelemetryClassic | 4.23K | ± 543.51 | ops/s |
| prometheusNative | 2.94K | ± 263.09 | ops/s |
| openTelemetryBoundExponential | 1.04K | ± 137.22 | ops/s |
| openTelemetryExponential | 902.08 | ± 30.05 | ops/s |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| openMetricsWriteToNull | 24.39K | ± 870.93 | ops/s |
| prometheusWriteToNull | 23.96K | ± 600.66 | ops/s |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusWriteToNull | 561.37K | ± 4.58K | ops/s |
| prometheusWriteToByteArray | 556.73K | ± 4.01K | ops/s |
| openMetricsWriteToNull | 532.71K | ± 3.80K | ops/s |
| openMetricsWriteToByteArray | 525.54K | ± 2.88K | ops/s |

## Allocation per operation

JMH GC profiler `gc.alloc.rate.norm`, in bytes per benchmark operation (lower is better).
Delta is PR minus base, shown only for matching benchmark configurations. Values are descriptive, not statistical regression verdicts; — means unavailable or not comparable. Each benchmark defines its own operation.

| Benchmark | PR B/op | Base B/op | Delta B/op |
|:----------|--------:|----------:|-----------:|
| CounterBenchmark.codahaleIncNoLabels | 0.019 | — | — |
| CounterBenchmark.openTelemetryAdd | 0.060 | — | — |
| CounterBenchmark.openTelemetryBoundAdd | 0.029 | — | — |
| CounterBenchmark.openTelemetryBoundInc | 0.025 | — | — |
| CounterBenchmark.openTelemetryInc | 0.052 | — | — |
| CounterBenchmark.openTelemetryIncNoLabels | 0.041 | — | — |
| CounterBenchmark.prometheusAdd | 0.072 | — | — |
| CounterBenchmark.prometheusCachedLabelValuesInc | 0.000 | — | — |
| CounterBenchmark.prometheusCachedLabelValuesIncSingleThread | 0.000 | — | — |
| CounterBenchmark.prometheusInc | 0.057 | — | — |
| CounterBenchmark.prometheusLabelValuesInc | 48.000 | — | — |
| CounterBenchmark.prometheusLabelValuesIncSingleThread | 48.000 | — | — |
| CounterBenchmark.prometheusNoLabelsInc | 0.065 | — | — |
| CounterBenchmark.simpleclientAdd | 0.144 | — | — |
| CounterBenchmark.simpleclientInc | 0.141 | — | — |
| CounterBenchmark.simpleclientNoLabelsInc | 0.146 | — | — |
| HistogramBenchmark.openTelemetryBoundClassic | 0.198 | — | — |
| HistogramBenchmark.openTelemetryBoundExponential | 0.906 | — | — |
| HistogramBenchmark.openTelemetryClassic | 0.223 | — | — |
| HistogramBenchmark.openTelemetryExponential | 1.028 | — | — |
| HistogramBenchmark.prometheusClassic | 0.592 | — | — |
| HistogramBenchmark.prometheusClassicPerThread | 0.665 | — | — |
| HistogramBenchmark.prometheusClassicSingleThread | 0.642 | — | — |
| HistogramBenchmark.prometheusNative | 335793.273 | — | — |
| HistogramBenchmark.simpleclient | 0.209 | — | — |
| HistogramTextFormatBenchmark.openMetricsWriteToNull | 43648.144 | — | — |
| HistogramTextFormatBenchmark.prometheusWriteToNull | 43648.146 | — | — |
| TextFormatUtilBenchmark.openMetricsWriteToByteArray | 18424.001 | — | — |
| TextFormatUtilBenchmark.openMetricsWriteToNull | 18424.001 | — | — |
| TextFormatUtilBenchmark.prometheusWriteToByteArray | 18448.001 | — | — |
| TextFormatUtilBenchmark.prometheusWriteToNull | 18466.668 | — | — |

### Raw Results

```text
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49460.836   ± 1076.286  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15      15573.604     ± 41.093  ops/s
CounterBenchmark.openTelemetryBoundAdd              thrpt   15      31837.080    ± 182.356  ops/s
CounterBenchmark.openTelemetryBoundInc              thrpt   15      37839.560    ± 403.841  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15      17999.686    ± 266.298  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15      22706.544   ± 1163.364  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51415.441    ± 158.391  ops/s
CounterBenchmark.prometheusCachedLabelValuesInc     thrpt   15  556552972.969 ± 5657236.471  ops/s
CounterBenchmark.prometheusCachedLabelValuesIncSingleThread  thrpt   15  334654019.551 ± 506321.486  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      64996.118   ± 1328.193  ops/s
CounterBenchmark.prometheusLabelValuesInc           thrpt   15  119299128.682 ± 1053421.477  ops/s
CounterBenchmark.prometheusLabelValuesIncSingleThread  thrpt   15   58529970.789 ± 179705.965  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56822.154    ± 331.089  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6438.321     ± 29.645  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6578.420     ± 13.315  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6328.476     ± 14.934  ops/s
HistogramBenchmark.openTelemetryBoundClassic        thrpt   15       5341.939   ± 1904.544  ops/s
HistogramBenchmark.openTelemetryBoundExponential    thrpt   15       1036.385    ± 137.218  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15       4226.154    ± 543.515  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        902.084     ± 30.052  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6301.505   ± 1004.457  ops/s
HistogramBenchmark.prometheusClassicPerThread       thrpt   15      12057.892     ± 18.963  ops/s
HistogramBenchmark.prometheusClassicSingleThread    thrpt   15       4537.193     ± 17.592  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2941.072    ± 263.091  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4430.870     ± 13.246  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      24390.001    ± 870.930  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      23957.122    ± 600.657  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     525541.454   ± 2875.504  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     532706.445   ± 3802.944  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     556728.580   ± 4013.287  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     561365.175   ± 4577.127  ops/s
```

## Notes

- **Score** = the JMH primary metric; throughput is higher-is-better and latency is lower-is-better.
- **Error** = 99.9% confidence interval
- Scores for different benchmark methods are not ranked against one another; they may measure different workloads.

## Benchmark Descriptions

| Benchmark | Description |
|:----------|:------------|
| **CounterBenchmark** | Counter updates and label-value lookup (selected methods only) |
| **HistogramBenchmark** | Histogram observation performance (classic vs native/exponential) |
| **TextFormatUtilBenchmark** | Metric exposition format writing speed |
