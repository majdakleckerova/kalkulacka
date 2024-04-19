# kalkulacka
TSW - 4. seminář 
1. vytvoření repozitáře "kalkulacka"
2. přidání kamarádů
3. vytvoření 3 issues, které si každý přiřadil
4. zkouška vytvoření větve a otevření v editoru (git fetch origin, git checkout "nazev vetve")
5. vytvoření projektu v repozitáři, "kalkulacka kanban tabule"
6. úprava kanban tabule ; Backlog -> Programming -> Ready for Testing -> Testing in process -> Testing Done
7. přidání items do Backlogu -> convert to issue -> programátor si je přiřadí -. přesune item do "Programming" , ....
8. poté co je vše hotovo, admin přesune funkce z větví na main - merge, pull request
9. vytvoření protection rule : repository -. settings -> branches -> protection rules -. název větve (main), "require a pull request before merging" , require approvals = 2
10. github action workflow , který při pushi spustí všechny pytestsoubory a řekne, zda pushnutý kód prošel testy: vytvořit skrytou složku .github/workflows/run_tests.yaml
workflow = sada co se spouští

11. toto napsat do yamlu:
 ```
  name: 
  on: [Push]
  jobs: 
    build: 
      runs-on: ubuntu-latest
      strategy:
        matrix:
          python-version: ["3.10","3.11"]
      steps:
        uses: actions/checkout@v3

        name: Nastav python
        uses: actions/setup-python@v4
        with:
          python-version: $(( matrix.python-version ))



        name: Nainstaluj zavislosti
        run: 
          python -m pip install pytest
          if [ -f requirement.txt ]; then pip install -r requirements.txt

        name: Otestuj kod pytestem
        run: pytest -v

        name: Otestuj pokryti
        run: pytest -cov
        
```          
    
