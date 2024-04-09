<!--
 * @Author: hibana2077 hibana2077@gmail.com
 * @Date: 2024-04-09 09:32:25
 * @LastEditors: hibana2077 hibana2077@gmail.com
 * @LastEditTime: 2024-04-09 14:06:56
 * @FilePath: \nttu_big_data_class_2024\lesson7\note.md
 * @Description: 这是默认设置,请设置`customMade`, 打开koroFileHeader查看配置 进行设置: https://github.com/OBKoro1/koro1FileHeader/wiki/%E9%85%8D%E7%BD%AE
-->
# Lesson 7: Spark

## 啟動 docker compose

```bash
docker-compose up -d
```

## 成功後，進入 spark-master 容器

```bash
docker exec -it lesson7_spark_1 bash
```

## 啟動 spark-shell

```bash
spark-shell
```