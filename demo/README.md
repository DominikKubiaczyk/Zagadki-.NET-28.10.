# Plan na wyklad nr 3 i pewnie 4
0. Pokazanie reguły routingu z własnym warunkiem na parametr -> MyRouteConstraint
1. Poprawna odpowiedź na pytanie zadane na poprzednim wykładzie w routingu - Kontroller Routing -> GetProduct
2. Prezentacja możliwości przyjecia danych z formularza z automatycznym wiązaniem wskazanych parametrów
3. Prezentacja możliwości przyjęcia danych w formacie JSON i zamiany ich na obiekt
4. Prezentacja właściwości klasy bazowej Controller -> ModelState - weryfikacja statusu walidacji
5. Prezentacja klasy z oznaczonymi metodami walidacji
6. Automatyczna serializacja danych na widoku do formatu JSON (csproj, startup, akcja) -> CatalogJson
7. Automatyczna serializacja danych na widoku do formatu XML (csproj, startup, klasa do serializacji, akcja) -> CatalogXml
8. Dynamiczne wskazywanie typu serializacji
9. Powrót do kontrollera "Ciasteczka" -> rozbudowa go do pełnego kontrolera dziedziczącego po Controller (Startup -> DI)
10. Zabawa w Routing dla akcji Reksio
---
11. Nachodzenie nazw kontrollerów - co zrobić? -> własny atrybut -> zmiana konwencji
12. Wreszcie jaka będzie nazwa akcji w kontrolerze zagnieżdżonym. Porównaj z SecondController
13. Może kiedyś uda się poprawić zmienną Catalog w RoutingController -> żeby zachowywała swój stan pomiędzy akcjami
14. Prosty sposób na filtrowanie akcji w kontrolerze: zbudujmy FilterController
15. Domyślne fabryki dostawców wartości - skąd mogą być czerpane wartości dla atrybutów (po nazwie)
16. Własna fabryka dostawców wartości - cookies (dostawca wartości -> fabryka -> startup)
17. Istniejące modele automatycznego wiązania -> sposób zamiany wartości z fabryk dostawców wartości na parametry akcji
18. Testowanie wiązania modeli
19. Token anulowania żądania asynchronicznego (przykład -> zadanie dodatkowe)
---
20. Różne typy predefiniowanych odpowiedzi IActionResult
21. Wersjonowanie API -> dependency, ApiVersion, Włączenie nagłówków startup/włączenie url, testy
22. Dodawanie automatycznie generowanej dokumentacji do API (OpenAPI) -> Dependencies (csproj), DI -> configureServices, modyfikacja middleware - poprawa projektu - -> uwaga!!
23. Zagadka (OpenAPI - API Versioning bez zmiany nazw) -> /swagger lub /swagger/v1/swagger.json 
24. Ręczne definiowanie parametrów Cache / Korzystanie z predefiniowanego profilu
25. Cookies
26. Sesja - włączenie - użycie
27. Cache odpowiedzi: DI -> dodanie instancji; middleware - dodanie komponentu 
28. Pamięć podręczna IMemoryCache
---
29. Pamięć podręczna IDistributedCache - włączenie Redis / włączenie SqlServer (włączenie serwera MSSQL: docker run -e 'ACCEPT_EULA=Y' -e 'SA_PASSWORD=STRONGpassword123' -p 1433:1433 -d mcr.microsoft.com/mssql/server:2017-latest) - (włączenie serwera REDIS: docker run 6379:6379 -d redis); -> CSPROJ -> DI -> CLI -> Kontroler
    1. Tworzenie nowej bazy w obrazie MS SQL: `/opt/mssql-tools/bin/sqlcmd -S localhost -U sa -P STRONGpassword123 -d master -i create-database.sql` gdzie create-database.sql: `CREATE DATABASE DistCache`
    2. `dotnet sql-cache create "Data Source=localhost;Initial Catalog=DistCache;User Id=sa; Password=STRONGpassword123;" dbo TestCache` 
    3. Zadanie -> docker-compose NGINX - test
30. Dane tymczasowe Cookie  -> DI ITempDataProvider (lub AddSession) -> Middleware UseSession -> Controller
31. Dane tymczasowe sesja
32. Sesja (DI DistributedMemoryCache lub inny; DI AddSesssion; Middleware UseSession)
33. Globalizacja (csproj MicrosoftAspNetCore.Localization.Routing) / DI AddLocalization / wspierane Kultury / jak rozróżniać którą kulturę zaoferować (header, cookie, query, route))
34. Globalizacja względem trasy (language:culture) -> własny warunek na ścieżkę / Configure<RouteOptions>
34. Lokalizacja (spróbujmy przetłumaczyć widoki) -> zagadka dlaczego Resources/plik.jezyk.resx nie działa - natomiast działa /Resources/Foldery/plik.jezyk.resx? - przechowanie parametru query między żądaniami
35. DataAnnotation Localization -> tłumaczenie komunikatów w formularzach (zadanie: z użyciem zasobów wspólnych)
---
36. Skąd pochodzą widoki - standardowo: plik cshtml, nazwa pliku identyczna jak nazwa widoku, przechowywane w folderze Views, w podfolderze odpowiadającym nazwie kontrolera, globalne widoki w Views/Shared -> my dodamy własną scieżkę AddRazorOptions -> pokazać możliwość tworzenia spersonalizowanych plików widoków dla języka (akcja bez widoku)
37. Ekspandery lokalizacji widoków -> AddRazorOptions -> options.ViewLocationExpanders -> własny expander
38. Podstawy składni Razor pętle/if 
---
39. Podstawy diagnostyki aplikacji
40. Kompilacja widoków / Własne kompilatory widoków
    1. `dotnet add package Microsoft.AspNetCore.mvc.Razor.ViewCompilation`
    2. plik csproj -> dodać do PropertyGroup `MvcRazorCompileOnPublish` oraz `PreserveCompilationContext`
    3. Widoki są prekompilowane podczas publikacji a nie kompilacji tzn. `dotnet publish`
41. Układy widoków -> Layout, partiale, komponenty 
42. 