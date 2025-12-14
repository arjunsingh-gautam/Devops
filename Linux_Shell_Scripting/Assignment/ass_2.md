# <span style="color:orange">Assignment-2</span>

## Q1.To display current system date in dd-mm-yyyy format.

```sh
date +%d-%m-%Y
```

## Q2. Create an empty file where file name contains current system date.

```sh
touch "backup$(date +%d%m%Y).log"
```

## Q3.Create an empty file where file name contains current system date and time

```sh
touch "backup$(date +%d%m%Y%H%M%S).log"
```
