# Azure Secrets Audit

### Regular Expressions to Search For Secrets

```sh
("|')?[0-9A-Fa-f]{8}-([0-9A-Fa-f]{4}-){3}[0-9A-Fa-f]{12}("|')?
("|')?.*[0-9a-zA-Z]{2,256}[.][o|O][n|N][m|M][i|I][c|C][r|R][o|O][s|S][o|O][f|F][t|T][.][c|C][o|O][m|M]("|')?
("|')?.*[0-9a-zA-Z]{2,256}[.][b|B][l|L][o|O][b|B][.][c|C][o|O][r|R][e|E][.][w|W][i|I][n|N][d|D][o|O][w|W][s|S][.][n|N][e|E][t|T]("|')?
("|')?(ARM|arm|Arm)?_?(CLIENT|client|Client)_(SECRET|secret|Secret)("|')?\s*(:|=>|=)\s*("|')?[A-Z0-9a-z[:punct:]]{34}("|')?
```

