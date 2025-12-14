## Q1.Case Study-1: Film Heroine's Manager

```
heroines
    sunny
        jan2020,feb2020,mar2020,......dec2022
    katrina
        jan2020,feb2020,mar2020,......dec2022
    kareena
        jan2020,feb2020,mar2020,......dec2022
```

```sh
mkdir heroines
cd heroines
mkdir sunny katrina kareena
mkdir {sunny,katrina,kareena}/{jan,feb,mar,apr,may,jun,jul,aug,sep,oct,nov,dec}_{2020,2021,2022}
```

## Q2.Create 5 directories named with dir6,dir7,dir8,dir9 and dir10. In these directories create empty files with a.txt,b.txt,c.txt and d.txt

```sh
mkdir dir{6..10}
touch dir{6..10}/{a..d}.txt
```
