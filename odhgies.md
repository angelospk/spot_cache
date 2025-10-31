Θέλω να χρησιμοποιήσεις τις υπάρχουσες συναρτήσεις που ενημερώνουν τη βάση δεδομένων, για μια νέα περίπτωση: αυτή τη φορά θα αλλάζουμε τα γενικά στοιχεία μιας αίτησης, θα προσθέτουμε δικαιολογητικά και πιθανώς μια δοκιμαστική σύμβαση μέσω κάποιου endpoint.

Η διαδικασία ενημέρωσης της βάσης είναι η ίδια, οπότε πρέπει να την ακολουθήσεις με τον ίδιο τρόπο. Οι παράμετροι που θα χρησιμοποιηθούν στα requests είναι σχεδόν οι ίδιοι με πριν.

Παρακάτω σου δίνω οδηγίες για τα νέα URLs και τη λογική που θα ακολουθείται: ποια requests θα εκτελούνται, πότε, και ποια δεδομένα θα προστίθενται στη βάση και σε ποιο στάδιο.

Η ιδέα είναι: πατώντας έναν συνδυασμό πλήκτρων (π.χ. Ctrl+M), θα εμφανίζεται ένα prompt για να δώσει ο χρήστης ένα JSON εισόδου. Αυτό το JSON θα περιέχει παραμέτρους με τιμές TRUE, FALSE ή NULL (δηλ δε θα υπάρχουν). Εμάς μας ενδιαφέρουν κυρίως οι τιμές TRUE. Αν δεν υπάρχουν ή είναι false είναι το ίδιο πρακτικά. Με βάση αυτές, θα καθορίζεται ποια requests θα γίνουν και ποιες οντότητες θα συμπεριληφθούν, ακολουθώντας τη λογική που περιγράφω. Επίσης θα περιέχει πληροφορίες για τις επωνυμίες και τα αφμ που θα χρειαστείς για τα τιμολόγια. Περιέγραψε μου πώς θα ήθελες να σου δίνεται αυτή η πληροφορία με τις επωνυμίες και τα δικαιολογητικά και φτιάξε τη λογική του κώδικα με βάση αυτή την περιγραφή. 


αρχικά θέλω να τραβάει τα στοιχεία gdpr κάνοντας αυτό το αίτημα:
## έλεγχος στοιχείων gdpr
curl 'https://eae2024.opekepe.gov.gr/eae2024/rest/MainService/refreshGdpr?' \
  -H 'accept: application/json, text/plain, */*' \
  -H 'accept-language: en-US,en;q=0.8' \
  -H 'cache-control: no-cache' \
  -H 'content-type: application/json' \
  -b 'eae2024-session-id=e2cdb26e-c8dc-456d-be5e-672d39fcf15c; eae2024-subs-code="mgm/lI1McsHlNZAQL4pXeE5h9sKGQleSBIiJgqSucCs="' \
  -H 'origin: https://eae2024.opekepe.gov.gr' \
  -H 'pragma: no-cache' \
  -H 'priority: u=1, i' \
  -H 'referer: https://eae2024.opekepe.gov.gr/eae2024/' \
  -H 'sec-ch-ua: "Brave";v="137", "Chromium";v="137", "Not/A)Brand";v="24"' \
  -H 'sec-ch-ua-mobile: ?0' \
  -H 'sec-ch-ua-platform: "Windows"' \
  -H 'sec-fetch-dest: empty' \
  -H 'sec-fetch-mode: cors' \
  -H 'sec-fetch-site: same-origin' \
  -H 'sec-gpc: 1' \
  -H 'user-agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/137.0.0.0 Safari/537.36' \
  --data-raw '{"edeId":"qB8ujfgfAKWoOF+W1gH/Ow==","etos":2025}'

## ελεγχος αναδιανεμητικης ενισχυσης:

curl 'https://eae2024.opekepe.gov.gr/eae2024/rest/Anadian/findAllByCriteriaRange_EdetedeaeehdGrpEdeAnadian' \
  -H 'accept: application/json, text/plain, */*' \
  -H 'accept-language: en-US,en;q=0.8' \
  -H 'cache-control: no-cache' \
  -H 'content-type: application/json' \
  -b 'eae2024-session-id=e2cdb26e-c8dc-456d-be5e-672d39fcf15c; eae2024-subs-code="mgm/lI1McsHlNZAQL4pXeE5h9sKGQleSBIiJgqSucCs="' \
  -H 'origin: https://eae2024.opekepe.gov.gr' \
  -H 'pragma: no-cache' \
  -H 'priority: u=1, i' \
  -H 'referer: https://eae2024.opekepe.gov.gr/eae2024/' \
  -H 'sec-ch-ua: "Brave";v="137", "Chromium";v="137", "Not/A)Brand";v="24"' \
  -H 'sec-ch-ua-mobile: ?0' \
  -H 'sec-ch-ua-platform: "Windows"' \
  -H 'sec-fetch-dest: empty' \
  -H 'sec-fetch-mode: cors' \
  -H 'sec-fetch-site: same-origin' \
  -H 'sec-gpc: 1' \
  -H 'user-agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/137.0.0.0 Safari/537.36' \
  --data-raw '{"edeId_id":"qB8ujfgfAKWoOF+W1gH/Ow==","fromRowIndex":0,"toRowIndex":10,"exc_Id":[]}'
  
απάντηση:
```json
{
    "count": -1,
    "data": [
        {
            "$entityName": "Anadian",
            "viewKey": "qB8ujfgfAKWoOF+W1gH/Ow==",
            "afm": null,
            "regionalType": null,
            "regDesc": null,
            "minEktash": null,
            "maxEktash": null,
            "priceHa": null,
            "factor": null,
            "dikaiomataflag": null,
            "regionArea": null,
            "reqionCnt": null,
            "isRegionWithinLimits": null,
            "withinLimitsCnt": null,
            "withinLimitsDikCnt": null,
            "totalArea": null,
            "totalEktashFactor": null,
            "anadianAmount": null,
            "errorMsg": null,
            "epileximosflag": null,
            "etos": 2025,
            "edeId": {
                "$entityName": "Edetedeaeehd",
                "id": "qB8ujfgfAKWoOF+W1gH/Ow==",
                "cuhId": null,
                "afm": "043409376",
                "recordtype": 0,
                "usrinsert": "app_prod_eae2327",
                "dteinsert": 1748984400000,
                "usrupdate": "app_prod_eae2327",
                "dteupdate": 1749675600000,
                "dtedelete": null,
                "prosopotype": 1,
                "name": null,
                "lastname": "ΑΣΦ",
                "firstname": "ΑΣΦΞΚ",
                "fathername": null,
                "odosB1": null,
                "numodosB1": null,
                "taxkodikosB1": "68300",
                "phone1B1": null,
                "mobilephoneB1": "6946571234",
                "idtype": null,
                "idno": null,
                "kodikos": 6311,
                "dteprotocol": null,
                "protocolarith": null,
                "gusrId": 1835589,
                "etos": 2025,
                "invalidrecordtype": 0,
                "remarks01": null,
                "remarks02": null,
                "remarks03": null,
                "email": "ava@gmail.com",
                "odosB2": null,
                "numodosB2": null,
                "taxkodikosB2": "68300",
                "topothesiaB2": null,
                "phone1B2": null,
                "iban": null,
                "ama": null,
                "amoga": null,
                "remarks": null,
                "bnkAccount": null,
                "remoteId": null,
                "remoteEfoId": null,
                "seiratype": 1,
                "dtebirth": 202856400000,
                "enoId": null,
                "arbibl": null,
                "remoteEdeId": null,
                "remoteEdeEfoId": null,
                "rejectFlag": null,
                "etosenteea": null,
                "p18qty": null,
                "sefoId": null,
                "downloadFlag": null,
                "amka": null,
                "entolheispflag": 1,
                "entolhxreflag": 0,
                "arkartaspolith": null,
                "mcoflag": 0,
                "genderflag": 2,
                "asfalishnumber": null,
                "dteasfalish": null,
                "metanastisflag": 0,
                "drasthriothtaflag": 0,
                "misthotisflag": 0,
                "ekmflag": 1,
                "dtestartekm": null,
                "arekm": null,
                "eidosekmtype": null,
                "fax": null,
                "eprotocolno": null,
                "asfaxiafytikovaluepro": 0,
                "asfaxiafytikovalue": 0,
                "asfaxiazoikovaluepro": 0,
                "asfaxiazoikovalue": 0,
                "eisforafytikovalue": 0,
                "eisforazoikovalue": 0,
                "eisfora1value": 0,
                "asfpercentchange": 0,
                "recordoltype": 0,
                "usrolId": null,
                "pendingelgaflag": 1,
                "dtedraststart": null,
                "dteonlineproseas": null,
                "rowVersion": 307,
                "prevyearid": null,
                "troposplhromhs": null,
                "troposypolxre": null,
                "exoterikoSynergioFlag": 0,
                "dtebirthvarchar": "06/06/1976",
                "gusrIdDik": null,
                "lastnameb": null,
                "sfflag": null,
                "sfapentaxhflag": null,
                "mobilephoneCountryCodeB1": 30,
                "egfkatflag": null,
                "bibliatype": null,
                "sfentaxhflag": null,
                "newflag": null,
                "youngflag": null,
                "ekmfirstyear": null,
                "eisforafytikovaluepro": 0,
                "eisforazoikovaluepro": 0,
                "nometabolesflag": null,
                "tritoprosopoflag": null,
                "allonpflag": null,
                "polithseeflag": null,
                "educationleveltype": null,
                "dteOris": null,
                "workAccessType": null,
                "mobilephoneCountryCodeB2": 30,
                "mobilephoneB2": null,
                "mothername": null,
                "daEtosPrevSum": null,
                "daEtosPrevEde": null,
                "daLtDaPrevFlag": null,
                "daLtDaPrevLhxh": null,
                "daLtDaPrevPolhsh": null,
                "businessGroupFlag": null,
                "kgpk7type": null,
                "edeIdPrev": null,
                "edeIdNext": null,
                "bnkId": null,
                "bnsId": null,
                "mcoKodikos": null,
                "orgId": null,
                "nmrId": null,
                "depId": null,
                "edeIdPraxis": null,
                "esapId": null,
                "edskId": null,
                "sfflagFinal": null,
                "lastEdaKodikos": null,
                "maxEdaaKodikos": null,
                "isCrmEnabled": null,
                "isEdeLfaFlag": null,
                "gusername": null,
                "mmzCalcValue": null,
                "efoDescription": null,
                "keaName": null
            }
        }
    ]
}
```

μας ενδιαφέρει το epileximosflag να είναι true. Αλλιώς δεν δικαιούται αναδιανεμητικη.


## υπάρχουσα μέτρα (αριθμος)

curl 'https://eae2024.opekepe.gov.gr/eae2024/rest/Edetedeaeepaa/findAllByCriteriaRange_EdetedeaeehdGrpEdaa_count' \
  -H 'accept: application/json, text/plain, */*' \
  -H 'accept-language: en-US,en;q=0.8' \
  -H 'cache-control: no-cache' \
  -H 'content-type: application/json' \
  -b 'eae2024-session-id=e2cdb26e-c8dc-456d-be5e-672d39fcf15c; eae2024-subs-code="mgm/lI1McsHlNZAQL4pXeE5h9sKGQleSBIiJgqSucCs="' \
  -H 'origin: https://eae2024.opekepe.gov.gr' \
  -H 'pragma: no-cache' \
  -H 'priority: u=1, i' \
  -H 'referer: https://eae2024.opekepe.gov.gr/eae2024/' \
  -H 'sec-ch-ua: "Brave";v="137", "Chromium";v="137", "Not/A)Brand";v="24"' \
  -H 'sec-ch-ua-mobile: ?0' \
  -H 'sec-ch-ua-platform: "Windows"' \
  -H 'sec-fetch-dest: empty' \
  -H 'sec-fetch-mode: cors' \
  -H 'sec-fetch-site: same-origin' \
  -H 'sec-gpc: 1' \
  -H 'user-agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/137.0.0.0 Safari/537.36' \
  --data-raw '{"edeId_id":"qB8ujfgfAKWoOF+W1gH/Ow==","gParams_yearEae":2025,"exc_Id":[]}'
  
  απάντηση (εδώ υπάρχει ένα,  η αποντριοποιήση):
```json
{
    "count": 1,
    "data": []
}
```

## υπάρχουσα αιτήματα άμεσων ενισχύσεων:
curl 'https://eae2024.opekepe.gov.gr/eae2024/rest/Edetedeaeerequest/findAllByCriteriaRange_EdetedeaeehdGrpEdrq_count' \
  -H 'accept: application/json, text/plain, */*' \
  -H 'accept-language: en-US,en;q=0.8' \
  -H 'cache-control: no-cache' \
  -H 'content-type: application/json' \
  -b 'eae2024-session-id=e2cdb26e-c8dc-456d-be5e-672d39fcf15c; eae2024-subs-code="mgm/lI1McsHlNZAQL4pXeE5h9sKGQleSBIiJgqSucCs="' \
  -H 'origin: https://eae2024.opekepe.gov.gr' \
  -H 'pragma: no-cache' \
  -H 'priority: u=1, i' \
  -H 'referer: https://eae2024.opekepe.gov.gr/eae2024/' \
  -H 'sec-ch-ua: "Brave";v="137", "Chromium";v="137", "Not/A)Brand";v="24"' \
  -H 'sec-ch-ua-mobile: ?0' \
  -H 'sec-ch-ua-platform: "Windows"' \
  -H 'sec-fetch-dest: empty' \
  -H 'sec-fetch-mode: cors' \
  -H 'sec-fetch-site: same-origin' \
  -H 'sec-gpc: 1' \
  -H 'user-agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/137.0.0.0 Safari/537.36' \
  --data-raw '{"edeId_id":"qB8ujfgfAKWoOF+W1gH/Ow==","gParams_yearEae":2025,"exc_Id":[]}'
  
απάντηση (συνήθως θα είναι ένα, το "0401" η βασική εισοδηματική στήριξη ):
```json
  {
    "count": 1,
    "data": []
}
```

## αίτημα για να λάβουμε τα ids από τα gdpr στοιχεία (για να μπορούμε να τα ανανεώσουμε στη συνέχεια):
curl 'https://eae2024.opekepe.gov.gr/eae2024/rest/Edetedeaeegdpr/findAllByCriteriaRange_EdetedeaeehdGrpEdgdpr' \
  -H 'accept: application/json, text/plain, */*' \
  -H 'accept-language: en-US,en;q=0.8' \
  -H 'cache-control: no-cache' \
  -H 'content-type: application/json' \
  -b 'eae2024-session-id=e2cdb26e-c8dc-456d-be5e-672d39fcf15c; eae2024-subs-code="mgm/lI1McsHlNZAQL4pXeE5h9sKGQleSBIiJgqSucCs="' \
  -H 'origin: https://eae2024.opekepe.gov.gr' \
  -H 'pragma: no-cache' \
  -H 'priority: u=1, i' \
  -H 'referer: https://eae2024.opekepe.gov.gr/eae2024/' \
  -H 'sec-ch-ua: "Brave";v="137", "Chromium";v="137", "Not/A)Brand";v="24"' \
  -H 'sec-ch-ua-mobile: ?0' \
  -H 'sec-ch-ua-platform: "Windows"' \
  -H 'sec-fetch-dest: empty' \
  -H 'sec-fetch-mode: cors' \
  -H 'sec-fetch-site: same-origin' \
  -H 'sec-gpc: 1' \
  -H 'user-agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/137.0.0.0 Safari/537.36' \
  --data-raw '{"edeId_id":"qB8ujfgfAKWoOF+W1gH/Ow==","gParams_yearEae":2025,"fromRowIndex":0,"toRowIndex":2000,"exc_Id":[]}'
  
απάντηση:
```json
{
    "count": -1,
    "data": [
        {
            "$entityName": "Edetedeaeegdpr",
            "id": "FWNmfW/yn1sFZmvSb/Kyqw==",
            "afm": "043409376",
            "recordtype": 0,
            "usrinsert": "app_prod_eae2327",
            "dteinsert": 1750107600000,
            "usrupdate": null,
            "dteupdate": null,
            "kodikos": 1,
            "sygkatatheshflag": null,
            "rowVersion": 0,
            "etos": 2025,
            "egdprKodikos": "2",
            "foreasDescription": "Τραπεζικά Ιδρύματα",
            "dataDescription": "Αποστολή στοιχείων δικαιωμάτων βασικής ενίσχυσης και μεταβιβάσεων δικαιωμάτων βασικής ενίσχυσης",
            "skoposDescription": "Διενέργεια ελέγχων προκειμένου να γίνει χορήγηση κάρτας αγρότη",
            "rolosDescription": "Υπεύθυνος επεξεργασίας",
            "epexDescription": null,
            "edeId": {
                "$entityName": "Edetedeaeehd",
                "id": "qB8ujfgfAKWoOF+W1gH/Ow==",
                "cuhId": null,
                "afm": "043409376",
                "recordtype": 0,
                "usrinsert": "app_prod_eae2327",
                "dteinsert": 1748984400000,
                "usrupdate": "app_prod_eae2327",
                "dteupdate": 1750107600000,
                "dtedelete": null,
                "prosopotype": 1,
                "name": null,
                "lastname": "ΑΣΦ",
                "firstname": "ΑΣΦΞΚ",
                "fathername": null,
                "odosB1": null,
                "numodosB1": null,
                "taxkodikosB1": "68300",
                "phone1B1": null,
                "mobilephoneB1": "6946571234",
                "idtype": null,
                "idno": null,
                "kodikos": 6311,
                "dteprotocol": null,
                "protocolarith": null,
                "gusrId": 1835589,
                "etos": 2025,
                "invalidrecordtype": 0,
                "remarks01": null,
                "remarks02": null,
                "remarks03": null,
                "email": "ava@gmail.com",
                "odosB2": null,
                "numodosB2": null,
                "taxkodikosB2": "68300",
                "topothesiaB2": null,
                "phone1B2": null,
                "iban": null,
                "ama": null,
                "amoga": null,
                "remarks": null,
                "bnkAccount": null,
                "remoteId": null,
                "remoteEfoId": null,
                "seiratype": 1,
                "dtebirth": 202856400000,
                "enoId": null,
                "arbibl": null,
                "remoteEdeId": null,
                "remoteEdeEfoId": null,
                "rejectFlag": null,
                "etosenteea": null,
                "p18qty": null,
                "sefoId": null,
                "downloadFlag": null,
                "amka": null,
                "entolheispflag": 0,
                "entolhxreflag": 0,
                "arkartaspolith": null,
                "mcoflag": 0,
                "genderflag": 2,
                "asfalishnumber": null,
                "dteasfalish": null,
                "metanastisflag": 0,
                "drasthriothtaflag": 0,
                "misthotisflag": 0,
                "ekmflag": 1,
                "dtestartekm": null,
                "arekm": null,
                "eidosekmtype": null,
                "fax": null,
                "eprotocolno": null,
                "asfaxiafytikovaluepro": 0,
                "asfaxiafytikovalue": 0,
                "asfaxiazoikovaluepro": 0,
                "asfaxiazoikovalue": 0,
                "eisforafytikovalue": 0,
                "eisforazoikovalue": 0,
                "eisfora1value": 0,
                "asfpercentchange": 0,
                "recordoltype": 0,
                "usrolId": null,
                "pendingelgaflag": 0,
                "dtedraststart": null,
                "dteonlineproseas": null,
                "rowVersion": 323,
                "prevyearid": null,
                "troposplhromhs": null,
                "troposypolxre": null,
                "exoterikoSynergioFlag": 0,
                "dtebirthvarchar": "06/06/1976",
                "gusrIdDik": null,
                "lastnameb": null,
                "sfflag": null,
                "sfapentaxhflag": null,
                "mobilephoneCountryCodeB1": 30,
                "egfkatflag": null,
                "bibliatype": null,
                "sfentaxhflag": null,
                "newflag": null,
                "youngflag": null,
                "ekmfirstyear": null,
                "eisforafytikovaluepro": 0,
                "eisforazoikovaluepro": 0,
                "nometabolesflag": null,
                "tritoprosopoflag": null,
                "allonpflag": null,
                "polithseeflag": null,
                "educationleveltype": null,
                "dteOris": null,
                "workAccessType": null,
                "mobilephoneCountryCodeB2": 30,
                "mobilephoneB2": null,
                "mothername": null,
                "daEtosPrevSum": null,
                "daEtosPrevEde": null,
                "daLtDaPrevFlag": null,
                "daLtDaPrevLhxh": null,
                "daLtDaPrevPolhsh": null,
                "businessGroupFlag": null,
                "kgpk7type": null,
                "edeIdPrev": null,
                "edeIdNext": null,
                "bnkId": null,
                "bnsId": null,
                "mcoKodikos": null,
                "orgId": null,
                "nmrId": null,
                "depId": null,
                "edeIdPraxis": null,
                "esapId": null,
                "edskId": null,
                "sfflagFinal": null,
                "lastEdaKodikos": null,
                "maxEdaaKodikos": null,
                "isCrmEnabled": null,
                "isEdeLfaFlag": null,
                "gusername": null,
                "mmzCalcValue": null,
                "efoDescription": null,
                "keaName": null
            }
        },
        {
            "$entityName": "Edetedeaeegdpr",
            "id": "Eb7689djkV7mp0ZCAugovg==",
            "afm": "043409376",
            "recordtype": 0,
            "usrinsert": "app_prod_eae2327",
            "dteinsert": 1750107600000,
            "usrupdate": null,
            "dteupdate": null,
            "kodikos": 2,
            "sygkatatheshflag": null,
            "rowVersion": 0,
            "etos": 2025,
            "egdprKodikos": "3",
            "foreasDescription": "Δήμοι",
            "dataDescription": "Στοιχεία δηλώσεων αιτήσεων ενιαίας ενίσχυσης και εκτάσεις κατανομής κοινοτικών βοσκοτόπων",
            "skoposDescription": "Διενέργεια ελέγχων και αναζήτηση τελών για βοσκήσιμες γαίες",
            "rolosDescription": "Υπεύθυνος επεξεργασίας",
            "epexDescription": null,
            "edeId": {
                "$entityName": "Edetedeaeehd",
                "$refId": "qB8ujfgfAKWoOF+W1gH/Ow=="
            }
        },
        {
            "$entityName": "Edetedeaeegdpr",
            "id": "cQxJAB18YCuKmvFX3pt9gw==",
            "afm": "043409376",
            "recordtype": 0,
            "usrinsert": "app_prod_eae2327",
            "dteinsert": 1750107600000,
            "usrupdate": null,
            "dteupdate": null,
            "kodikos": 3,
            "sygkatatheshflag": null,
            "rowVersion": 0,
            "etos": 2025,
            "egdprKodikos": "9",
            "foreasDescription": "Ενώσεις / συνεταιρισμοί παραγωγών",
            "dataDescription": "Σύνολο στοιχείων επιδοτήσεων για τους παραγωγούς αρμοδιότητας του φορέα",
            "skoposDescription": "Λειτουργία ένωσης παραγωγών",
            "rolosDescription": "Υπεύθυνος επεξεργασίας",
            "epexDescription": null,
            "edeId": {
                "$entityName": "Edetedeaeehd",
                "$refId": "qB8ujfgfAKWoOF+W1gH/Ow=="
            }
        },
        {
            "$entityName": "Edetedeaeegdpr",
            "id": "b9IkgMEj6vJnkq0bTvx6hg==",
            "afm": "043409376",
            "recordtype": 0,
            "usrinsert": "app_prod_eae2327",
            "dteinsert": 1750107600000,
            "usrupdate": null,
            "dteupdate": null,
            "kodikos": 4,
            "sygkatatheshflag": null,
            "rowVersion": 0,
            "etos": 2025,
            "egdprKodikos": "10",
            "foreasDescription": "ΔΕΗ Ανανεώσιμες Α.Ε.",
            "dataDescription": "Χορήγηση στοιχείων ψηφιακών γεωχωρικών δεδομένων για καμένη έκταση σε διάφορα Τοπικά διαμερίσματα",
            "skoposDescription": "Αποκατάσταση πληγέντων παραγωγών",
            "rolosDescription": "Υπεύθυνος επεξεργασίας",
            "epexDescription": null,
            "edeId": {
                "$entityName": "Edetedeaeehd",
                "$refId": "qB8ujfgfAKWoOF+W1gH/Ow=="
            }
        },
        {
            "$entityName": "Edetedeaeegdpr",
            "id": "WFCAP35SSWEnvB7oXI9cWA==",
            "afm": "043409376",
            "recordtype": 0,
            "usrinsert": "app_prod_eae2327",
            "dteinsert": 1750107600000,
            "usrupdate": null,
            "dteupdate": null,
            "kodikos": 5,
            "sygkatatheshflag": null,
            "rowVersion": 0,
            "etos": 2025,
            "egdprKodikos": "11",
            "foreasDescription": "Επιμελητήριο",
            "dataDescription": "Στοιχεία παραγωγών φυτικού και ζωϊκού κεφαλαίου",
            "skoposDescription": "Στήριξη της κτηνοτροφικής / φυτικής παραγωγής και σύνδεση με δευτερογενή τομέα",
            "rolosDescription": "Υπεύθυνος επεξεργασίας",
            "epexDescription": null,
            "edeId": {
                "$entityName": "Edetedeaeehd",
                "$refId": "qB8ujfgfAKWoOF+W1gH/Ow=="
            }
        },
        {
            "$entityName": "Edetedeaeegdpr",
            "id": "IFQGkyqqGMkoIZKPbx9Xng==",
            "afm": "043409376",
            "recordtype": 0,
            "usrinsert": "app_prod_eae2327",
            "dteinsert": 1750107600000,
            "usrupdate": null,
            "dteupdate": null,
            "kodikos": 6,
            "sygkatatheshflag": null,
            "rowVersion": 0,
            "etos": 2025,
            "egdprKodikos": "13",
            "foreasDescription": "Αγροτικοί συνεταιρισμοί / ομάδες παραγωγών",
            "dataDescription": "Στοιχεία αιτήσεων παραγωγών",
            "skoposDescription": "Επικαιροποίηση μητρώου μελών",
            "rolosDescription": "Υπεύθυνος επεξεργασίας",
            "epexDescription": null,
            "edeId": {
                "$entityName": "Edetedeaeehd",
                "$refId": "qB8ujfgfAKWoOF+W1gH/Ow=="
            }
        },
        {
            "$entityName": "Edetedeaeegdpr",
            "id": "5hKsYO7muNhHe6A3DtXPtg==",
            "afm": "043409376",
            "recordtype": 0,
            "usrinsert": "app_prod_eae2327",
            "dteinsert": 1750107600000,
            "usrupdate": null,
            "dteupdate": null,
            "kodikos": 7,
            "sygkatatheshflag": null,
            "rowVersion": 0,
            "etos": 2025,
            "egdprKodikos": "14",
            "foreasDescription": "Κτηνοτροφικοί σύλλογοι",
            "dataDescription": "Στοιχεία επικοινωνίας  παραγωγών/αιτήσεων κτηνοτρόφων",
            "skoposDescription": "Επικοινωνία για ενημέρωση σχετικά με ασθένειες ζώων και αδειοδότηση κτηνοτροφικών εγκαταστάσεων",
            "rolosDescription": "Υπεύθυνος επεξεργασίας",
            "epexDescription": null,
            "edeId": {
                "$entityName": "Edetedeaeehd",
                "$refId": "qB8ujfgfAKWoOF+W1gH/Ow=="
            }
        },
        {
            "$entityName": "Edetedeaeegdpr",
            "id": "mWLMy1Hb5Ff8k/v6InXExQ==",
            "afm": "043409376",
            "recordtype": 0,
            "usrinsert": "app_prod_eae2327",
            "dteinsert": 1750107600000,
            "usrupdate": null,
            "dteupdate": null,
            "kodikos": 8,
            "sygkatatheshflag": null,
            "rowVersion": 0,
            "etos": 2025,
            "egdprKodikos": "15",
            "foreasDescription": "Αγροτικοί συνεταιρισμοί / ομάδες παραγωγών",
            "dataDescription": "Στοιχεία αιτήσεων παραγωγών",
            "skoposDescription": "Συμμετοχή σε προγράμματα",
            "rolosDescription": "Υπεύθυνος επεξεργασίας",
            "epexDescription": null,
            "edeId": {
                "$entityName": "Edetedeaeehd",
                "$refId": "qB8ujfgfAKWoOF+W1gH/Ow=="
            }
        },
        {
            "$entityName": "Edetedeaeegdpr",
            "id": "pxoSAxLK6G9BvoZa00YxeA==",
            "afm": "043409376",
            "recordtype": 0,
            "usrinsert": "app_prod_eae2327",
            "dteinsert": 1750107600000,
            "usrupdate": null,
            "dteupdate": null,
            "kodikos": 9,
            "sygkatatheshflag": null,
            "rowVersion": 0,
            "etos": 2025,
            "egdprKodikos": "16",
            "foreasDescription": "Δήμοι",
            "dataDescription": "Στοιχεία αιτήσεων παραγωγών που περιέχουν τη δήλωση φυτικού και ζωϊκού κεφαλαίου",
            "skoposDescription": "Δημιουργία βάσης δεδομένων με τις εκτάσεις και τις αγροτικές εκμεταλλεύσεις",
            "rolosDescription": "Υπεύθυνος επεξεργασίας",
            "epexDescription": "Περαιτέρω επεξεργασία",
            "edeId": {
                "$entityName": "Edetedeaeehd",
                "$refId": "qB8ujfgfAKWoOF+W1gH/Ow=="
            }
        },
        {
            "$entityName": "Edetedeaeegdpr",
            "id": "SMxzCndxGdDHFGZMR0TljQ==",
            "afm": "043409376",
            "recordtype": 0,
            "usrinsert": "app_prod_eae2327",
            "dteinsert": 1750107600000,
            "usrupdate": null,
            "dteupdate": null,
            "kodikos": 10,
            "sygkatatheshflag": null,
            "rowVersion": 0,
            "etos": 2025,
            "egdprKodikos": "17",
            "foreasDescription": "Πανεπιστήμια / ερευνητικά ιδρύματα",
            "dataDescription": "Χορήγηση στοιχείων παραγωγών/αιτήσεων/γεωχωρικών δεδομένων",
            "skoposDescription": "Ερευνητικά προγράμματα",
            "rolosDescription": "Υπεύθυνος επεξεργασίας",
            "epexDescription": "Περαιτέρω επεξεργασία",
            "edeId": {
                "$entityName": "Edetedeaeehd",
                "$refId": "qB8ujfgfAKWoOF+W1gH/Ow=="
            }
        },
        {
            "$entityName": "Edetedeaeegdpr",
            "id": "BOC0SvPTXA/r1oWps0tkDQ==",
            "afm": "043409376",
            "recordtype": 0,
            "usrinsert": "app_prod_eae2327",
            "dteinsert": 1750107600000,
            "usrupdate": null,
            "dteupdate": null,
            "kodikos": 11,
            "sygkatatheshflag": null,
            "rowVersion": 0,
            "etos": 2025,
            "egdprKodikos": "18",
            "foreasDescription": "Κτηματολόγιο Α.Ε.",
            "dataDescription": "Αποστολή προσωπικών στοιχείων και στοιχείων αγροτεμαχίων",
            "skoposDescription": "Χρήση δεδομένων για την προσυμπλήρωση της Ηλεκτρονικής Δήλωσης Κτηματολογίου",
            "rolosDescription": "Υπεύθυνος επεξεργασίας",
            "epexDescription": "Περαιτέρω επεξεργασία",
            "edeId": {
                "$entityName": "Edetedeaeehd",
                "$refId": "qB8ujfgfAKWoOF+W1gH/Ow=="
            }
        },
        {
            "$entityName": "Edetedeaeegdpr",
            "id": "UzXFkpUzNx4BgEYNRdKBpQ==",
            "afm": "043409376",
            "recordtype": 0,
            "usrinsert": "app_prod_eae2327",
            "dteinsert": 1750107600000,
            "usrupdate": null,
            "dteupdate": null,
            "kodikos": 12,
            "sygkatatheshflag": null,
            "rowVersion": 0,
            "etos": 2025,
            "egdprKodikos": "19",
            "foreasDescription": "ΔΕΔΔΗΕ Α.Ε. (Διαχειριστής του Ελληνικού Δικτύου Διανομής Ηλεκτρικής Ενέργειας)",
            "dataDescription": "Αποστολή προσωπικών στοιχείων, αγροτεμαχίων, αριθμού παροχών ηλεκτρικού ρεύματος και στοιχεία ιδιοκτητών",
            "skoposDescription": "Επεξεργασία δεδομένων για μειωμένο αγροτικό τιμολόγιο στο ρεύμα",
            "rolosDescription": "Υπεύθυνος επεξεργασίας",
            "epexDescription": "Περαιτέρω επεξεργασία",
            "edeId": {
                "$entityName": "Edetedeaeehd",
                "$refId": "qB8ujfgfAKWoOF+W1gH/Ow=="
            }
        },
        {
            "$entityName": "Edetedeaeegdpr",
            "id": "PD1l1q4renVctUR14jyV1g==",
            "afm": "043409376",
            "recordtype": 0,
            "usrinsert": "app_prod_eae2327",
            "dteinsert": 1750107600000,
            "usrupdate": null,
            "dteupdate": null,
            "kodikos": 13,
            "sygkatatheshflag": null,
            "rowVersion": 0,
            "etos": 2025,
            "egdprKodikos": "20",
            "foreasDescription": "Πάροχοι ηλεκτρικού ρεύματος",
            "dataDescription": "Αποστολή προσωπικών στοιχείων, αγροτεμαχίων, αριθμού παροχών ηλεκτρικού ρεύματος και στοιχεία ιδιοκτητών",
            "skoposDescription": "Επεξεργασία δεδομένων για μειωμένο αγροτικό τιμολόγιο στο ρεύμα",
            "rolosDescription": "Υπεύθυνος επεξεργασίας",
            "epexDescription": "Περαιτέρω επεξεργασία",
            "edeId": {
                "$entityName": "Edetedeaeehd",
                "$refId": "qB8ujfgfAKWoOF+W1gH/Ow=="
            }
        },
        {
            "$entityName": "Edetedeaeegdpr",
            "id": "oXHLKh8wNEC7/aUlnFsrNw==",
            "afm": "043409376",
            "recordtype": 0,
            "usrinsert": "app_prod_eae2327",
            "dteinsert": 1750107600000,
            "usrupdate": null,
            "dteupdate": null,
            "kodikos": 14,
            "sygkatatheshflag": null,
            "rowVersion": 0,
            "etos": 2025,
            "egdprKodikos": "21",
            "foreasDescription": "Ειδική Υπηρεσία Διαχείρισης ΣΣ ΚΑΠ της Γενικής Γραμματείας Ενωσιακών Πόρων και Υποδομών",
            "dataDescription": "Στοιχεία επικοινωνίας παραγωγών",
            "skoposDescription": "Ενημέρωση παραγωγών για ευκαιρίες χρηματοδότησης, καθώς και για ενέργειες δημοσιότητας/εκδηλώσεις που υλοποιούνται είτε από τις Ειδικές Υπηρεσίες του ΣΣ ΚΑΠ, είτε από το EU CAP NETWORK",
            "rolosDescription": null,
            "epexDescription": null,
            "edeId": {
                "$entityName": "Edetedeaeehd",
                "$refId": "qB8ujfgfAKWoOF+W1gH/Ow=="
            }
        }
    ]
}
```


## μαζικό αίτημα ανανέωσης γενικών στοιχείων αίτησης
url: https://eae2024.opekepe.gov.gr/eae2024/rest/MainService/synchronizeChangesWithDb_Edetedeaeehd
method: post
requst body:
```json
[
    {
        "status": 1,
        "when": 1750184340857,
        "entityName": "Edetedeaeehd",
        "entity": {
            "id": "qB8ujfgfAKWoOF+W1gH/Ow==",
            "cuhId": null,
            "afm": "043409376",
            "recordtype": 0,
            "usrinsert": "app_prod_eae2327",
            "dteinsert": "2025-06-03T21:00:00.000Z",
            "usrupdate": "app_prod_eae2327",
            "dteupdate": "2025-06-16T21:00:00.000Z",
            "dtedelete": null,
            "prosopotype": 1,
            "name": null,
            "lastname": "ΑΣΦ",
            "firstname": "ΑΣΦΞΚ",
            "fathername": null,
            "odosB1": null,
            "numodosB1": null,
            "taxkodikosB1": "68300",
            "phone1B1": null,
            "mobilephoneB1": "6946571234",
            "idtype": null,
            "idno": null,
            "kodikos": 6311,
            "dteprotocol": null,
            "protocolarith": null,
            "gusrId": 1835589,
            "etos": 2025,
            "invalidrecordtype": 0,
            "remarks01": null,
            "remarks02": null,
            "remarks03": null,
            "email": "ava@gmail.com",
            "odosB2": null,
            "numodosB2": null,
            "taxkodikosB2": "68300",
            "topothesiaB2": null,
            "phone1B2": null,
            "iban": null,
            "ama": null,
            "amoga": null,
            "remarks": null,
            "bnkAccount": null,
            "remoteId": null,
            "remoteEfoId": null,
            "seiratype": 1,
            "dtebirth": "1976-06-05T21:00:00.000Z",
            "enoId": null,
            "arbibl": null,
            "remoteEdeId": null,
            "remoteEdeEfoId": null,
            "rejectFlag": null,
            "etosenteea": null,
            "p18qty": null,
            "sefoId": null,
            "downloadFlag": null,
            "amka": null,
            "entolheispflag": 1,
            "entolhxreflag": 0,
            "arkartaspolith": null,
            "mcoflag": 0,
            "genderflag": 2,
            "asfalishnumber": null,
            "dteasfalish": null,
            "metanastisflag": 0,
            "drasthriothtaflag": 0,
            "misthotisflag": 0,
            "ekmflag": 1,
            "dtestartekm": null,
            "arekm": null,
            "eidosekmtype": null,
            "fax": null,
            "eprotocolno": null,
            "asfaxiafytikovaluepro": 0,
            "asfaxiafytikovalue": 0,
            "asfaxiazoikovaluepro": 0,
            "asfaxiazoikovalue": 0,
            "eisforafytikovalue": 0,
            "eisforazoikovalue": 0,
            "eisfora1value": 0,
            "asfpercentchange": 0,
            "recordoltype": 0,
            "usrolId": null,
            "pendingelgaflag": 1,
            "dtedraststart": null,
            "dteonlineproseas": null,
            "rowVersion": 323,
            "prevyearid": null,
            "troposplhromhs": null,
            "troposypolxre": null,
            "exoterikoSynergioFlag": 0,
            "dtebirthvarchar": "06/06/1976",
            "gusrIdDik": null,
            "lastnameb": null,
            "sfflag": null,
            "sfapentaxhflag": null,
            "mobilephoneCountryCodeB1": 30,
            "egfkatflag": null,
            "bibliatype": null,
            "sfentaxhflag": null,
            "newflag": null,
            "youngflag": null,
            "ekmfirstyear": null,
            "eisforafytikovaluepro": 0,
            "eisforazoikovaluepro": 0,
            "nometabolesflag": null,
            "tritoprosopoflag": null,
            "allonpflag": null,
            "polithseeflag": null,
            "educationleveltype": null,
            "dteOris": null,
            "workAccessType": null,
            "mobilephoneCountryCodeB2": 30,
            "mobilephoneB2": null,
            "mothername": null,
            "daEtosPrevSum": null,
            "daEtosPrevEde": null,
            "daLtDaPrevFlag": null,
            "daLtDaPrevLhxh": null,
            "daLtDaPrevPolhsh": null,
            "businessGroupFlag": 0,
            "kgpk7type": null,
            "lkkoiIdB1": {
                "id": "047Hbgu7JmwDEeqFuXq//Q=="
            },
            "doyId": {
                "id": "bXS36x7gfMJVrdFwh0hNrg=="
            },
            "efoId": {
                "id": "Iw+H52J9KNTxmT/GRBgcSw=="
            },
            "lkpenIdA": {
                "id": "8QM7lFNZ9FKoQ8ukjdCFzA=="
            },
            "lkpenIdB1": {
                "id": "8QM7lFNZ9FKoQ8ukjdCFzA=="
            },
            "lkpenIdB2": {
                "id": "8QM7lFNZ9FKoQ8ukjdCFzA=="
            },
            "lkkoiIdB2": {
                "id": "047Hbgu7JmwDEeqFuXq//Q=="
            },
            "daokKodikos": {
                "kodikos": "EoWHUsY6N/biOzW7pPm+Aw=="
            },
            "opdId": {
                "id": "WuzMVOxRhelo8bsXch2Qwg=="
            },
            "ddsId": {
                "id": "Q+miKtIOtZZDH9VJa9Q5Ug=="
            },
            "ddrId": {
                "id": "YQZshL1w5CJDVzyTeSQedA=="
            },
            "lkprfId": {
                "id": "xoaTOHC7dea7wsFLV5rsjg=="
            },
            "mcoKodikos": null,
            "lkprfIdB2": {
                "id": "xoaTOHC7dea7wsFLV5rsjg=="
            },
            "nmrId": null,
            "ownerSexId": {
                "id": "99gZmMPS9BTTkHuUFInwyw=="
            },
            "sexId": {
                "id": "99gZmMPS9BTTkHuUFInwyw=="
            },
            "sfflagFinal": null,
            "lastEdaKodikos": 0,
            "maxEdaaKodikos": 1,
            "isCrmEnabled": null,
            "isEdeLfaFlag": 2,
            "gusername": "ΒΑΒΑΛΟΥ ΑΡΤΕΜΗΣΙΑ",
            "mmzCalcValue": null,
            "efoDescription": "ONLINE_TAXIS_USERS",
            "keaName": "ONLINE_TAXIS_USERS"
        }
    },
    {
        "status": 0,
        "when": 1750185500082,
        "entityName": "Edetedeaeerequest",
        "entity": {
            "id": "TEMP_ID_19",
            "afm": "043409376",
            "recordtype": 0,
            "usrinsert": null,
            "dteinsert": null,
            "usrupdate": null,
            "dteupdate": null,
            "kodikos": 5,
            "eschLt2": 2,
            "zoa": null,
            "remarks": null,
            "rowVersion": null,
            "mmz": null,
            "declareWaterFlag": null,
            "etos": 2025,
            "declareAmpelFlag": null,
            "edeId": {
                "id": "qB8ujfgfAKWoOF+W1gH/Ow=="
            },
            "eschId": {
                "id": "n8FWQG78kWo4DWgzxWdpow=="
            },
            "sexId": {
                "id": "99gZmMPS9BTTkHuUFInwyw=="
            },
            "sporosqtyEdrqsSum": null,
            "etiketesEdrqsSum": null
        }
    },
    {
        "status": 0,
        "when": 1750185349841,
        "entityName": "Edetedeaeerequest",
        "entity": {
            "id": "TEMP_ID_16",
            "afm": "043409376",
            "recordtype": 0,
            "usrinsert": null,
            "dteinsert": null,
            "usrupdate": null,
            "dteupdate": null,
            "kodikos": 4,
            "eschLt2": 2,
            "zoa": null,
            "remarks": null,
            "rowVersion": null,
            "mmz": null,
            "declareWaterFlag": null,
            "etos": 2025,
            "declareAmpelFlag": null,
            "edeId": {
                "id": "qB8ujfgfAKWoOF+W1gH/Ow=="
            },
            "eschId": {
                "id": "hU7dS7bG1ZMN/5Zz98Yjkg=="
            },
            "sexId": {
                "id": "99gZmMPS9BTTkHuUFInwyw=="
            },
            "sporosqtyEdrqsSum": null,
            "etiketesEdrqsSum": null
        }
    },
    {
        "status": 0,
        "when": 1750184508594,
        "entityName": "Edetedeaeerequest",
        "entity": {
            "id": "TEMP_ID_13",
            "afm": "043409376",
            "recordtype": 0,
            "usrinsert": null,
            "dteinsert": null,
            "usrupdate": null,
            "dteupdate": null,
            "kodikos": 3,
            "eschLt2": 2,
            "zoa": null,
            "remarks": null,
            "rowVersion": null,
            "mmz": null,
            "declareWaterFlag": null,
            "etos": 2025,
            "declareAmpelFlag": null,
            "edeId": {
                "id": "qB8ujfgfAKWoOF+W1gH/Ow=="
            },
            "eschId": {
                "id": "3u1xdPE4FZAqQT4Pm2e4tQ=="
            },
            "sexId": {
                "id": "99gZmMPS9BTTkHuUFInwyw=="
            },
            "sporosqtyEdrqsSum": null,
            "etiketesEdrqsSum": null
        }
    },
    {
        "status": 0,
        "when": 1750184483672,
        "entityName": "Edetedeaeerequest",
        "entity": {
            "id": "TEMP_ID_12",
            "afm": "043409376",
            "recordtype": 0,
            "usrinsert": null,
            "dteinsert": null,
            "usrupdate": null,
            "dteupdate": null,
            "kodikos": 2,
            "eschLt2": 2,
            "zoa": null,
            "remarks": null,
            "rowVersion": null,
            "mmz": null,
            "declareWaterFlag": null,
            "etos": 2025,
            "declareAmpelFlag": null,
            "edeId": {
                "id": "qB8ujfgfAKWoOF+W1gH/Ow=="
            },
            "eschId": {
                "id": "tuDUgj3HP7PZZCh/70Ro/w=="
            },
            "sexId": {
                "id": "99gZmMPS9BTTkHuUFInwyw=="
            },
            "sporosqtyEdrqsSum": null,
            "etiketesEdrqsSum": null
        }
    },
    {
        "status": 0,
        "when": 1750185522586,
        "entityName": "Edetedeaeerequestsporo",
        "entity": {
            "id": "TEMP_ID_21",
            "afm": "043409376",
            "recordtype": 0,
            "usrinsert": null,
            "dteinsert": null,
            "usrupdate": null,
            "dteupdate": null,
            "kodikos": 1,
            "remarks": null,
            "rowVersion": null,
            "sporosqty": 100,
            "etiketes": 5,
            "sporosnum": null,
            "etos": 2025,
            "edeId": {
                "id": "qB8ujfgfAKWoOF+W1gH/Ow=="
            },
            "edrqId": {
                "id": "TEMP_ID_19"
            },
            "eschId": {
                "id": "n8FWQG78kWo4DWgzxWdpow=="
            },
            "sexId": {
                "id": "99gZmMPS9BTTkHuUFInwyw=="
            },
            "efyId": {
                "id": "78sdEMOgHjUYxJHA+vgG+g=="
            },
            "poiId": {
                "id": "/Kw9TbsKdLaah9jFsBXIeA=="
            }
        }
    },
    {
        "status": 0,
        "when": 1750185447289,
        "entityName": "Edetedeaeerequestsporo",
        "entity": {
            "id": "TEMP_ID_17",
            "afm": "043409376",
            "recordtype": 0,
            "usrinsert": null,
            "dteinsert": null,
            "usrupdate": null,
            "dteupdate": null,
            "kodikos": 1,
            "remarks": null,
            "rowVersion": null,
            "sporosqty": 100,
            "etiketes": 5,
            "sporosnum": null,
            "etos": 2025,
            "edeId": {
                "id": "qB8ujfgfAKWoOF+W1gH/Ow=="
            },
            "edrqId": {
                "id": "TEMP_ID_16"
            },
            "eschId": {
                "id": "hU7dS7bG1ZMN/5Zz98Yjkg=="
            },
            "sexId": {
                "id": "99gZmMPS9BTTkHuUFInwyw=="
            },
            "efyId": {
                "id": "Zu50wPtrta9nV1CJTP3nkQ=="
            },
            "poiId": {
                "id": "iOkQVQUJWEdzY0IzwErItg=="
            }
        }
    },
    {
        "status": 0,
        "when": 1750184967230,
        "entityName": "Edetedeaeerequestsporo",
        "entity": {
            "id": "TEMP_ID_14",
            "afm": "043409376",
            "recordtype": 0,
            "usrinsert": null,
            "dteinsert": null,
            "usrupdate": null,
            "dteupdate": null,
            "kodikos": 1,
            "remarks": null,
            "rowVersion": null,
            "sporosqty": 100,
            "etiketes": 5,
            "sporosnum": null,
            "etos": 2025,
            "edeId": {
                "id": "qB8ujfgfAKWoOF+W1gH/Ow=="
            },
            "edrqId": {
                "id": "9uFQYJTdsgj6nSzjMuQFQg=="
            },
            "eschId": {
                "id": "sIEDL+QVuQh+iX+oOTWZQw=="
            },
            "efyId": {
                "id": "VMxnJnQisDYspssypbAjjA=="
            },
            "poiId": {
                "id": "Zu50wPtrta9nV1CJTP3nkQ=="
            }
        }
    },
    {
        "status": 0,
        "when": 1750185511571,
        "entityName": "Edetedeaeerequestinvoice",
        "entity": {
            "id": "TEMP_ID_20",
            "afm": "043409376",
            "kodikos": 1,
            "timologioafm": "096049221",
            "timologioafm2": null,
            "timologioname": "ΕΝΩΣΗ ΑΓΡΟΤΙΚΩΝ ΣΥΝΕΤΑΙΡΙΣΜΩΝ ΟΡΕΣΤΙΑΔΑΣ",
            "timologiono": null,
            "timologioseira": null,
            "timologiodte": "2024-12-31T22:00:00.000Z",
            "remarks": null,
            "recordtype": 0,
            "usrinsert": null,
            "dteinsert": null,
            "usrupdate": null,
            "dteupdate": null,
            "rowVersion": null,
            "etos": 2025,
            "edeId": {
                "id": "qB8ujfgfAKWoOF+W1gH/Ow=="
            },
            "edrqId": {
                "id": "TEMP_ID_19"
            },
            "sexId": {
                "id": "99gZmMPS9BTTkHuUFInwyw=="
            }
        }
    },
    {
        "status": 0,
        "when": 1750185487875,
        "entityName": "Edetedeaeerequestinvoice",
        "entity": {
            "id": "TEMP_ID_18",
            "afm": "043409376",
            "kodikos": 1,
            "timologioafm": "096049221",
            "timologioafm2": null,
            "timologioname": "ΕΝΩΣΗ ΑΓΡΟΤΙΚΩΝ ΣΥΝΕΤΑΙΡΙΣΜΩΝ ΟΡΕΣΤΙΑΔΑΣ",
            "timologiono": null,
            "timologioseira": null,
            "timologiodte": "2024-12-31T22:00:00.000Z",
            "remarks": null,
            "recordtype": 0,
            "usrinsert": null,
            "dteinsert": null,
            "usrupdate": null,
            "dteupdate": null,
            "rowVersion": null,
            "etos": 2025,
            "edeId": {
                "id": "qB8ujfgfAKWoOF+W1gH/Ow=="
            },
            "edrqId": {
                "id": "TEMP_ID_16"
            },
            "sexId": {
                "id": "99gZmMPS9BTTkHuUFInwyw=="
            }
        }
    },
    {
        "status": 0,
        "when": 1750185019405,
        "entityName": "Edetedeaeerequestinvoice",
        "entity": {
            "id": "TEMP_ID_15",
            "afm": "043409376",
            "kodikos": 1,
            "timologioafm": "096049221",
            "timologioafm2": null,
            "timologioname": "ΕΝΩΣΗ ΑΓΡΟΤΙΚΩΝ ΣΥΝΕΤΑΙΡΙΣΜΩΝ ΟΡΕΣΤΙΑΔΑΣ",
            "timologiono": null,
            "timologioseira": null,
            "timologiodte": "2024-12-31T22:00:00.000Z",
            "remarks": null,
            "recordtype": 0,
            "usrinsert": null,
            "dteinsert": null,
            "usrupdate": null,
            "dteupdate": null,
            "rowVersion": null,
            "etos": 2025,
            "edeId": {
                "id": "qB8ujfgfAKWoOF+W1gH/Ow=="
            },
            "edrqId": {
                "id": "9uFQYJTdsgj6nSzjMuQFQg=="
            }
        }
    },
    {
        "status": 0,
        "when": 1750185977103,
        "entityName": "Edetedeaeeeco",
        "entity": {
            "id": "TEMP_ID_25",
            "afm": "043409376",
            "recordtype": 0,
            "usrinsert": null,
            "dteinsert": null,
            "usrupdate": null,
            "dteupdate": null,
            "kodikos": 2,
            "remarks": null,
            "rowVersion": null,
            "idioparagomenosflag": null,
            "etos": 2025,
            "polyethsflag": null,
            "edeId": {
                "id": "qB8ujfgfAKWoOF+W1gH/Ow=="
            },
            "esgrId": {
                "id": "idonCkcn3mDYtA6vW3X5pg=="
            },
            "sexId": {
                "id": "99gZmMPS9BTTkHuUFInwyw=="
            }
        }
    },
    {
        "status": 0,
        "when": 1750185904845,
        "entityName": "Edetedeaeeeco",
        "entity": {
            "id": "TEMP_ID_22",
            "afm": "043409376",
            "recordtype": 0,
            "usrinsert": null,
            "dteinsert": null,
            "usrupdate": null,
            "dteupdate": null,
            "kodikos": 1,
            "remarks": null,
            "rowVersion": null,
            "idioparagomenosflag": null,
            "etos": 2025,
            "polyethsflag": null,
            "edeId": {
                "id": "qB8ujfgfAKWoOF+W1gH/Ow=="
            },
            "esgrId": {
                "id": "ck7Q9Gq/UBkTwjID7Ur4vg=="
            },
            "sexId": {
                "id": "99gZmMPS9BTTkHuUFInwyw=="
            }
        }
    },
    {
        "status": 0,
        "when": 1750185956198,
        "entityName": "Edetedeaeeecoinvoice",
        "entity": {
            "id": "TEMP_ID_24",
            "afm": "043409376",
            "kodikos": 2,
            "timologioafm": "096049221",
            "timologioafm2": null,
            "timologioname": "ΕΝΩΣΗ ΑΓΡΟΤΙΚΩΝ ΣΥΝΕΤΑΙΡΙΣΜΩΝ ΟΡΕΣΤΙΑΔΑΣ",
            "timologiono": null,
            "timologioseira": null,
            "timologiodte": "2024-12-31T22:00:00.000Z",
            "remarks": null,
            "recordtype": 0,
            "usrinsert": null,
            "dteinsert": null,
            "usrupdate": null,
            "dteupdate": null,
            "rowVersion": null,
            "etos": 2025,
            "edeId": {
                "id": "qB8ujfgfAKWoOF+W1gH/Ow=="
            },
            "edegId": {
                "id": "TEMP_ID_22"
            },
            "sexId": {
                "id": "99gZmMPS9BTTkHuUFInwyw=="
            }
        }
    },
    {
        "status": 0,
        "when": 1750185948695,
        "entityName": "Edetedeaeeecoinvoice",
        "entity": {
            "id": "TEMP_ID_23",
            "afm": "043409376",
            "kodikos": 1,
            "timologioafm": "096049221",
            "timologioafm2": null,
            "timologioname": "ΕΝΩΣΗ ΑΓΡΟΤΙΚΩΝ ΣΥΝΕΤΑΙΡΙΣΜΩΝ ΟΡΕΣΤΙΑΔΑΣ",
            "timologiono": null,
            "timologioseira": null,
            "timologiodte": "2024-12-31T22:00:00.000Z",
            "remarks": null,
            "recordtype": 0,
            "usrinsert": null,
            "dteinsert": null,
            "usrupdate": null,
            "dteupdate": null,
            "rowVersion": null,
            "etos": 2025,
            "edeId": {
                "id": "qB8ujfgfAKWoOF+W1gH/Ow=="
            },
            "edegId": {
                "id": "TEMP_ID_22"
            },
            "sexId": {
                "id": "99gZmMPS9BTTkHuUFInwyw=="
            }
        }
    },
    {
        "status": 1,
        "when": 1750186056999,
        "entityName": "Edetedeaeegdpr",
        "entity": {
            "id": "FWNmfW/yn1sFZmvSb/Kyqw==",
            "afm": "043409376",
            "recordtype": 0,
            "usrinsert": "app_prod_eae2327",
            "dteinsert": "2025-06-16T21:00:00.000Z",
            "usrupdate": null,
            "dteupdate": null,
            "kodikos": 1,
            "sygkatatheshflag": 1,
            "rowVersion": 0,
            "etos": 2025,
            "egdprKodikos": "2",
            "foreasDescription": "Τραπεζικά Ιδρύματα",
            "dataDescription": "Αποστολή στοιχείων δικαιωμάτων βασικής ενίσχυσης και μεταβιβάσεων δικαιωμάτων βασικής ενίσχυσης",
            "skoposDescription": "Διενέργεια ελέγχων προκειμένου να γίνει χορήγηση κάρτας αγρότη",
            "rolosDescription": "Υπεύθυνος επεξεργασίας",
            "epexDescription": null,
            "edeId": {
                "id": "qB8ujfgfAKWoOF+W1gH/Ow=="
            }
        }
    },
    {
        "status": 1,
        "when": 1750186056999,
        "entityName": "Edetedeaeegdpr",
        "entity": {
            "id": "Eb7689djkV7mp0ZCAugovg==",
            "afm": "043409376",
            "recordtype": 0,
            "usrinsert": "app_prod_eae2327",
            "dteinsert": "2025-06-16T21:00:00.000Z",
            "usrupdate": null,
            "dteupdate": null,
            "kodikos": 2,
            "sygkatatheshflag": 1,
            "rowVersion": 0,
            "etos": 2025,
            "egdprKodikos": "3",
            "foreasDescription": "Δήμοι",
            "dataDescription": "Στοιχεία δηλώσεων αιτήσεων ενιαίας ενίσχυσης και εκτάσεις κατανομής κοινοτικών βοσκοτόπων",
            "skoposDescription": "Διενέργεια ελέγχων και αναζήτηση τελών για βοσκήσιμες γαίες",
            "rolosDescription": "Υπεύθυνος επεξεργασίας",
            "epexDescription": null,
            "edeId": {
                "id": "qB8ujfgfAKWoOF+W1gH/Ow=="
            }
        }
    },
    {
        "status": 1,
        "when": 1750186056999,
        "entityName": "Edetedeaeegdpr",
        "entity": {
            "id": "cQxJAB18YCuKmvFX3pt9gw==",
            "afm": "043409376",
            "recordtype": 0,
            "usrinsert": "app_prod_eae2327",
            "dteinsert": "2025-06-16T21:00:00.000Z",
            "usrupdate": null,
            "dteupdate": null,
            "kodikos": 3,
            "sygkatatheshflag": 1,
            "rowVersion": 0,
            "etos": 2025,
            "egdprKodikos": "9",
            "foreasDescription": "Ενώσεις / συνεταιρισμοί παραγωγών",
            "dataDescription": "Σύνολο στοιχείων επιδοτήσεων για τους παραγωγούς αρμοδιότητας του φορέα",
            "skoposDescription": "Λειτουργία ένωσης παραγωγών",
            "rolosDescription": "Υπεύθυνος επεξεργασίας",
            "epexDescription": null,
            "edeId": {
                "id": "qB8ujfgfAKWoOF+W1gH/Ow=="
            }
        }
    },
    {
        "status": 1,
        "when": 1750186056999,
        "entityName": "Edetedeaeegdpr",
        "entity": {
            "id": "b9IkgMEj6vJnkq0bTvx6hg==",
            "afm": "043409376",
            "recordtype": 0,
            "usrinsert": "app_prod_eae2327",
            "dteinsert": "2025-06-16T21:00:00.000Z",
            "usrupdate": null,
            "dteupdate": null,
            "kodikos": 4,
            "sygkatatheshflag": 1,
            "rowVersion": 0,
            "etos": 2025,
            "egdprKodikos": "10",
            "foreasDescription": "ΔΕΗ Ανανεώσιμες Α.Ε.",
            "dataDescription": "Χορήγηση στοιχείων ψηφιακών γεωχωρικών δεδομένων για καμένη έκταση σε διάφορα Τοπικά διαμερίσματα",
            "skoposDescription": "Αποκατάσταση πληγέντων παραγωγών",
            "rolosDescription": "Υπεύθυνος επεξεργασίας",
            "epexDescription": null,
            "edeId": {
                "id": "qB8ujfgfAKWoOF+W1gH/Ow=="
            }
        }
    },
    {
        "status": 1,
        "when": 1750186056999,
        "entityName": "Edetedeaeegdpr",
        "entity": {
            "id": "WFCAP35SSWEnvB7oXI9cWA==",
            "afm": "043409376",
            "recordtype": 0,
            "usrinsert": "app_prod_eae2327",
            "dteinsert": "2025-06-16T21:00:00.000Z",
            "usrupdate": null,
            "dteupdate": null,
            "kodikos": 5,
            "sygkatatheshflag": 1,
            "rowVersion": 0,
            "etos": 2025,
            "egdprKodikos": "11",
            "foreasDescription": "Επιμελητήριο",
            "dataDescription": "Στοιχεία παραγωγών φυτικού και ζωϊκού κεφαλαίου",
            "skoposDescription": "Στήριξη της κτηνοτροφικής / φυτικής παραγωγής και σύνδεση με δευτερογενή τομέα",
            "rolosDescription": "Υπεύθυνος επεξεργασίας",
            "epexDescription": null,
            "edeId": {
                "id": "qB8ujfgfAKWoOF+W1gH/Ow=="
            }
        }
    },
    {
        "status": 1,
        "when": 1750186056999,
        "entityName": "Edetedeaeegdpr",
        "entity": {
            "id": "IFQGkyqqGMkoIZKPbx9Xng==",
            "afm": "043409376",
            "recordtype": 0,
            "usrinsert": "app_prod_eae2327",
            "dteinsert": "2025-06-16T21:00:00.000Z",
            "usrupdate": null,
            "dteupdate": null,
            "kodikos": 6,
            "sygkatatheshflag": 1,
            "rowVersion": 0,
            "etos": 2025,
            "egdprKodikos": "13",
            "foreasDescription": "Αγροτικοί συνεταιρισμοί / ομάδες παραγωγών",
            "dataDescription": "Στοιχεία αιτήσεων παραγωγών",
            "skoposDescription": "Επικαιροποίηση μητρώου μελών",
            "rolosDescription": "Υπεύθυνος επεξεργασίας",
            "epexDescription": null,
            "edeId": {
                "id": "qB8ujfgfAKWoOF+W1gH/Ow=="
            }
        }
    },
    {
        "status": 1,
        "when": 1750186056999,
        "entityName": "Edetedeaeegdpr",
        "entity": {
            "id": "5hKsYO7muNhHe6A3DtXPtg==",
            "afm": "043409376",
            "recordtype": 0,
            "usrinsert": "app_prod_eae2327",
            "dteinsert": "2025-06-16T21:00:00.000Z",
            "usrupdate": null,
            "dteupdate": null,
            "kodikos": 7,
            "sygkatatheshflag": 1,
            "rowVersion": 0,
            "etos": 2025,
            "egdprKodikos": "14",
            "foreasDescription": "Κτηνοτροφικοί σύλλογοι",
            "dataDescription": "Στοιχεία επικοινωνίας  παραγωγών/αιτήσεων κτηνοτρόφων",
            "skoposDescription": "Επικοινωνία για ενημέρωση σχετικά με ασθένειες ζώων και αδειοδότηση κτηνοτροφικών εγκαταστάσεων",
            "rolosDescription": "Υπεύθυνος επεξεργασίας",
            "epexDescription": null,
            "edeId": {
                "id": "qB8ujfgfAKWoOF+W1gH/Ow=="
            }
        }
    },
    {
        "status": 1,
        "when": 1750186056999,
        "entityName": "Edetedeaeegdpr",
        "entity": {
            "id": "mWLMy1Hb5Ff8k/v6InXExQ==",
            "afm": "043409376",
            "recordtype": 0,
            "usrinsert": "app_prod_eae2327",
            "dteinsert": "2025-06-16T21:00:00.000Z",
            "usrupdate": null,
            "dteupdate": null,
            "kodikos": 8,
            "sygkatatheshflag": 1,
            "rowVersion": 0,
            "etos": 2025,
            "egdprKodikos": "15",
            "foreasDescription": "Αγροτικοί συνεταιρισμοί / ομάδες παραγωγών",
            "dataDescription": "Στοιχεία αιτήσεων παραγωγών",
            "skoposDescription": "Συμμετοχή σε προγράμματα",
            "rolosDescription": "Υπεύθυνος επεξεργασίας",
            "epexDescription": null,
            "edeId": {
                "id": "qB8ujfgfAKWoOF+W1gH/Ow=="
            }
        }
    },
    {
        "status": 1,
        "when": 1750186057000,
        "entityName": "Edetedeaeegdpr",
        "entity": {
            "id": "pxoSAxLK6G9BvoZa00YxeA==",
            "afm": "043409376",
            "recordtype": 0,
            "usrinsert": "app_prod_eae2327",
            "dteinsert": "2025-06-16T21:00:00.000Z",
            "usrupdate": null,
            "dteupdate": null,
            "kodikos": 9,
            "sygkatatheshflag": 1,
            "rowVersion": 0,
            "etos": 2025,
            "egdprKodikos": "16",
            "foreasDescription": "Δήμοι",
            "dataDescription": "Στοιχεία αιτήσεων παραγωγών που περιέχουν τη δήλωση φυτικού και ζωϊκού κεφαλαίου",
            "skoposDescription": "Δημιουργία βάσης δεδομένων με τις εκτάσεις και τις αγροτικές εκμεταλλεύσεις",
            "rolosDescription": "Υπεύθυνος επεξεργασίας",
            "epexDescription": "Περαιτέρω επεξεργασία",
            "edeId": {
                "id": "qB8ujfgfAKWoOF+W1gH/Ow=="
            }
        }
    },
    {
        "status": 1,
        "when": 1750186057000,
        "entityName": "Edetedeaeegdpr",
        "entity": {
            "id": "SMxzCndxGdDHFGZMR0TljQ==",
            "afm": "043409376",
            "recordtype": 0,
            "usrinsert": "app_prod_eae2327",
            "dteinsert": "2025-06-16T21:00:00.000Z",
            "usrupdate": null,
            "dteupdate": null,
            "kodikos": 10,
            "sygkatatheshflag": 1,
            "rowVersion": 0,
            "etos": 2025,
            "egdprKodikos": "17",
            "foreasDescription": "Πανεπιστήμια / ερευνητικά ιδρύματα",
            "dataDescription": "Χορήγηση στοιχείων παραγωγών/αιτήσεων/γεωχωρικών δεδομένων",
            "skoposDescription": "Ερευνητικά προγράμματα",
            "rolosDescription": "Υπεύθυνος επεξεργασίας",
            "epexDescription": "Περαιτέρω επεξεργασία",
            "edeId": {
                "id": "qB8ujfgfAKWoOF+W1gH/Ow=="
            }
        }
    },
    {
        "status": 1,
        "when": 1750186057000,
        "entityName": "Edetedeaeegdpr",
        "entity": {
            "id": "BOC0SvPTXA/r1oWps0tkDQ==",
            "afm": "043409376",
            "recordtype": 0,
            "usrinsert": "app_prod_eae2327",
            "dteinsert": "2025-06-16T21:00:00.000Z",
            "usrupdate": null,
            "dteupdate": null,
            "kodikos": 11,
            "sygkatatheshflag": 1,
            "rowVersion": 0,
            "etos": 2025,
            "egdprKodikos": "18",
            "foreasDescription": "Κτηματολόγιο Α.Ε.",
            "dataDescription": "Αποστολή προσωπικών στοιχείων και στοιχείων αγροτεμαχίων",
            "skoposDescription": "Χρήση δεδομένων για την προσυμπλήρωση της Ηλεκτρονικής Δήλωσης Κτηματολογίου",
            "rolosDescription": "Υπεύθυνος επεξεργασίας",
            "epexDescription": "Περαιτέρω επεξεργασία",
            "edeId": {
                "id": "qB8ujfgfAKWoOF+W1gH/Ow=="
            }
        }
    },
    {
        "status": 1,
        "when": 1750186057000,
        "entityName": "Edetedeaeegdpr",
        "entity": {
            "id": "UzXFkpUzNx4BgEYNRdKBpQ==",
            "afm": "043409376",
            "recordtype": 0,
            "usrinsert": "app_prod_eae2327",
            "dteinsert": "2025-06-16T21:00:00.000Z",
            "usrupdate": null,
            "dteupdate": null,
            "kodikos": 12,
            "sygkatatheshflag": 1,
            "rowVersion": 0,
            "etos": 2025,
            "egdprKodikos": "19",
            "foreasDescription": "ΔΕΔΔΗΕ Α.Ε. (Διαχειριστής του Ελληνικού Δικτύου Διανομής Ηλεκτρικής Ενέργειας)",
            "dataDescription": "Αποστολή προσωπικών στοιχείων, αγροτεμαχίων, αριθμού παροχών ηλεκτρικού ρεύματος και στοιχεία ιδιοκτητών",
            "skoposDescription": "Επεξεργασία δεδομένων για μειωμένο αγροτικό τιμολόγιο στο ρεύμα",
            "rolosDescription": "Υπεύθυνος επεξεργασίας",
            "epexDescription": "Περαιτέρω επεξεργασία",
            "edeId": {
                "id": "qB8ujfgfAKWoOF+W1gH/Ow=="
            }
        }
    },
    {
        "status": 1,
        "when": 1750186057000,
        "entityName": "Edetedeaeegdpr",
        "entity": {
            "id": "PD1l1q4renVctUR14jyV1g==",
            "afm": "043409376",
            "recordtype": 0,
            "usrinsert": "app_prod_eae2327",
            "dteinsert": "2025-06-16T21:00:00.000Z",
            "usrupdate": null,
            "dteupdate": null,
            "kodikos": 13,
            "sygkatatheshflag": 1,
            "rowVersion": 0,
            "etos": 2025,
            "egdprKodikos": "20",
            "foreasDescription": "Πάροχοι ηλεκτρικού ρεύματος",
            "dataDescription": "Αποστολή προσωπικών στοιχείων, αγροτεμαχίων, αριθμού παροχών ηλεκτρικού ρεύματος και στοιχεία ιδιοκτητών",
            "skoposDescription": "Επεξεργασία δεδομένων για μειωμένο αγροτικό τιμολόγιο στο ρεύμα",
            "rolosDescription": "Υπεύθυνος επεξεργασίας",
            "epexDescription": "Περαιτέρω επεξεργασία",
            "edeId": {
                "id": "qB8ujfgfAKWoOF+W1gH/Ow=="
            }
        }
    },
    {
        "status": 1,
        "when": 1750186057000,
        "entityName": "Edetedeaeegdpr",
        "entity": {
            "id": "oXHLKh8wNEC7/aUlnFsrNw==",
            "afm": "043409376",
            "recordtype": 0,
            "usrinsert": "app_prod_eae2327",
            "dteinsert": "2025-06-16T21:00:00.000Z",
            "usrupdate": null,
            "dteupdate": null,
            "kodikos": 14,
            "sygkatatheshflag": 1,
            "rowVersion": 0,
            "etos": 2025,
            "egdprKodikos": "21",
            "foreasDescription": "Ειδική Υπηρεσία Διαχείρισης ΣΣ ΚΑΠ της Γενικής Γραμματείας Ενωσιακών Πόρων και Υποδομών",
            "dataDescription": "Στοιχεία επικοινωνίας παραγωγών",
            "skoposDescription": "Ενημέρωση παραγωγών για ευκαιρίες χρηματοδότησης, καθώς και για ενέργειες δημοσιότητας/εκδηλώσεις που υλοποιούνται είτε από τις Ειδικές Υπηρεσίες του ΣΣ ΚΑΠ, είτε από το EU CAP NETWORK",
            "rolosDescription": null,
            "epexDescription": null,
            "edeId": {
                "id": "qB8ujfgfAKWoOF+W1gH/Ow=="
            }
        }
    }
]

```
απάντηση:
```json
{
    "newEntitiesIds": [
        {
            "entityName": "Edetedeaeeeco",
            "tempId": "TEMP_ID_22",
            "databaseId": "T6+6aU83kyugLRNmqLyfyA=="
        },
        {
            "entityName": "Edetedeaeerequestsporo",
            "tempId": "TEMP_ID_21",
            "databaseId": "edOQszM6bm8r3xSfkRVgMA=="
        },
        ...
    ],
    "warningMessages": null,
    "infoMessages": null
}
```

Εξήγηση παραμέτρων αιτήματος και λογική δημιουργίας τους:
1) στην έδρα εκμετάλλευσης, βάζουμε 'όχι' στο συμμετοχή σε όμιλο επιχειρήσεων:
2) στην ασφαλιστική εισφορά, βάζουμε ΝΑΙ, ΟΧΙ, ΝΑΙ
3) ΑΝ υπάρχει θετική παράμετρος στην είσοδο για εξισωτική, προσθέτουμε τα μέτρα της εξισωτικής (3 συνολικά) τα 13.1, 13.2, 13.3 στο ήδη υπάρχον μέτρο αν υπάρχει. Και 
4) ΑΝ ο χρήστης είναι επιλεξιμος για αναδιανεμητικη ενίσχυση (δες πιο πάνω), την προσθετουμε στις αμεσες ενισχυσεις
ΠΑΝΤΑ ΘΑ ΒΑΖΕΙΣ ΕΣΤΩ ΕΝΑ ΔΟΚΙΜΑΣΤΙΚΟ ΤΙΜΟΛΟΓΙΟ ΚΑΙ ΜΙΑ ΔΟΚΙΜΑΣΤΙΚΗ ΚΑΛΛΙΡΕΓΕΙΑ ΜΕ ΤΥΧΑΙΑ ΚΙΛΑ ΣΤΙΣ ΣΥΝΔΕΔΕΜΕΝΕΣ
5) ΑΝ υπάρχει θετική παράμετρος στην είσοδο σκληρό σίτο, προσθέτουμε τη συνδεδεμένη. Επίσης στην είσοδο θα υπάρχει πληροφορία για το πόσα τιμολόγια υπάρχουν για την καλλιέργεια, και απο ποια εταιρεία είναι αγορασμένα. Εσυ θα τα προσθεσεις αναλογα στα αντιστοιχα πεδια. Στο παραδειγμα εδω θα βαλω "ΕΝΩΣΗ ΑΓΡΟΤΙΚΩΝ ΣΥΝΕΤΑΙΡΙΣΜΩΝ ΟΡΕΣΤΙΑΔΑΣ" για επωνυμια και 096049221 για αφμ με μια τυχαια ημερομηνια. Επισης θα υπαρχει και ενα τεστ στοιχειο οπου καταχωρειται η ποικιλια και βαζουμε συνολικα κιλα και ετικετες. Εγω θα βαλω για παραδειγμα την ποικιλια MARAKAS με 100 κιλά και 5 ετικέτες. Θα βάζουμε κάτι παρόμοιο και θα το αλλάζω μετά εγώ χειροκίνητα.
6) ΑΝ υπάρχει θετική παράμετρος στην είσοδο για μαλακό σίτο, προσθέτουμε τη συνδεδεμένη μαλακού σίτου. Αντίστοιχα βάζω ένα δοκιμαστικό τιμολόγιο να δεις πως μπαίνει, και βαζω δοκιμαστικη ποικιλια sicario 100 κιλά, 5 ετικέτες
7) ΑΝ υπάρχει θετική παράμετρος στην είσοδο για βαμβάκι, προσθέτουμε τη συνδεδεμένη. Παλι βαζω δοκιμαστικα ενα τιμολογιο, και προσθετω ως τεστ την ποικιλια "ZETA 2" 100 κιλά 5 ετικέτες
Στα οικολογικά σχήματα τώρα:
8) ΑΝ υπάρχει θετική παράμετρος για το μέτρο με τα λιπάσματα, το προσθέτω. Εδώ για παράδειγμα το έβαλα, είναι στην ομάδα Ι και βάζω και δυο τιμολόγια ενδεικτικά και αυτά από την ενωση ορεστιάδας
9) ΑΝ υπάρχει θετική παράμετρος για το βιολογικό σχήμα, το προσθέτω. Εδώ το έβαλα για παράδειγμα επίσης. ΔΕΝ ΘΕΛΕΙ ΤΙΜΟΛΟΓΙΟ ΑΥΤΟ.

Τέλος, βάζουμε ΝΑΙ σε όλα στα δικαιώματα GDPR. 
Και έτσι ολοκλήρωνονται τα γενικά στοιχεία της αίτησης.

## Στη συνέχεια:
ΑΝ υπάρχει θετική παράμετρος για σύμβαση ηλίανθου, πηγαίνουμε και καταχωρούμε μια τυπική στανταρ σύμβαση κάνοντας αυτό το αίτημα:
url: https://eae2024.opekepe.gov.gr/eae2024/rest/MainService/synchronizeChangesWithDb_Edetedeaeemetcom
method: POST

request body:
```json
{
    "params": {
        "data": [
            {
                "status": 0,
                "when": 1750186813298,
                "entityName": "Edetedeaeemetcom",
                "entity": {
                    "id": "TEMP_ID_26",
                    "afm": "043409376",
                    "recordtype": 0,
                    "usrinsert": null,
                    "dteinsert": null,
                    "usrupdate": null,
                    "dteupdate": null,
                    "kodikos": 1,
                    "remarks": null,
                    "sexId": null,
                    "arsymbashmet": "1",
                    "dtesymbashmet": "2024-12-31T22:00:00.000Z",
                    "rowVersion": null,
                    "contractektash": 1,
                    "etos": 2025,
                    "edeId": {
                        "id": "qB8ujfgfAKWoOF+W1gH/Ow=="
                    },
                    "emcId": {
                        "id": "KTSgRe2sSLggaN9qu8u/Pg=="
                    },
                    "efecId": {
                        "id": "WFUwa5UO57dxpXhnvqIKRA=="
                    }
                }
            },
            {
                "status": 1,
                "when": 0,
                "entityName": "Edetedeaeehd",
                "entity": {
                    "id": "qB8ujfgfAKWoOF+W1gH/Ow==",
                    "cuhId": null,
                    "afm": "043409376",
                    "recordtype": 0,
                    "usrinsert": "app_prod_eae2327",
                    "dteinsert": "2025-06-03T21:00:00.000Z",
                    "usrupdate": "app_prod_eae2327",
                    "dteupdate": "2025-06-16T21:00:00.000Z",
                    "dtedelete": null,
                    "prosopotype": 1,
                    "name": null,
                    "lastname": "ΑΣΦ",
                    "firstname": "ΑΣΦΞΚ",
                    "fathername": null,
                    "odosB1": null,
                    "numodosB1": null,
                    "taxkodikosB1": "68300",
                    "phone1B1": null,
                    "mobilephoneB1": "6946571234",
                    "idtype": null,
                    "idno": null,
                    "kodikos": 6311,
                    "dteprotocol": null,
                    "protocolarith": null,
                    "gusrId": 1835589,
                    "etos": 2025,
                    "invalidrecordtype": 0,
                    "remarks01": null,
                    "remarks02": null,
                    "remarks03": null,
                    "email": "ava@gmail.com",
                    "odosB2": null,
                    "numodosB2": null,
                    "taxkodikosB2": "68300",
                    "topothesiaB2": null,
                    "phone1B2": null,
                    "iban": null,
                    "ama": null,
                    "amoga": null,
                    "remarks": null,
                    "bnkAccount": null,
                    "remoteId": null,
                    "remoteEfoId": null,
                    "seiratype": 1,
                    "dtebirth": "1976-06-05T21:00:00.000Z",
                    "enoId": null,
                    "arbibl": null,
                    "remoteEdeId": null,
                    "remoteEdeEfoId": null,
                    "rejectFlag": null,
                    "etosenteea": null,
                    "p18qty": null,
                    "sefoId": null,
                    "downloadFlag": null,
                    "amka": null,
                    "entolheispflag": 1,
                    "entolhxreflag": 0,
                    "arkartaspolith": null,
                    "mcoflag": 0,
                    "genderflag": 2,
                    "asfalishnumber": null,
                    "dteasfalish": null,
                    "metanastisflag": 0,
                    "drasthriothtaflag": 0,
                    "misthotisflag": 0,
                    "ekmflag": 1,
                    "dtestartekm": null,
                    "arekm": null,
                    "eidosekmtype": null,
                    "fax": null,
                    "eprotocolno": null,
                    "asfaxiafytikovaluepro": 0,
                    "asfaxiafytikovalue": 0,
                    "asfaxiazoikovaluepro": 0,
                    "asfaxiazoikovalue": 0,
                    "eisforafytikovalue": 0,
                    "eisforazoikovalue": 0,
                    "eisfora1value": 0,
                    "asfpercentchange": 0,
                    "recordoltype": 0,
                    "usrolId": null,
                    "pendingelgaflag": 1,
                    "dtedraststart": null,
                    "dteonlineproseas": null,
                    "rowVersion": 329,
                    "prevyearid": null,
                    "troposplhromhs": null,
                    "troposypolxre": null,
                    "exoterikoSynergioFlag": 0,
                    "dtebirthvarchar": "06/06/1976",
                    "gusrIdDik": null,
                    "lastnameb": null,
                    "sfflag": null,
                    "sfapentaxhflag": null,
                    "mobilephoneCountryCodeB1": 30,
                    "egfkatflag": null,
                    "bibliatype": null,
                    "sfentaxhflag": null,
                    "newflag": null,
                    "youngflag": null,
                    "ekmfirstyear": null,
                    "eisforafytikovaluepro": 0,
                    "eisforazoikovaluepro": 0,
                    "nometabolesflag": null,
                    "tritoprosopoflag": null,
                    "allonpflag": null,
                    "polithseeflag": null,
                    "educationleveltype": null,
                    "dteOris": null,
                    "workAccessType": null,
                    "mobilephoneCountryCodeB2": 30,
                    "mobilephoneB2": null,
                    "mothername": null,
                    "daEtosPrevSum": null,
                    "daEtosPrevEde": null,
                    "daLtDaPrevFlag": null,
                    "daLtDaPrevLhxh": null,
                    "daLtDaPrevPolhsh": null,
                    "businessGroupFlag": 0,
                    "kgpk7type": null,
                    "lkkoiIdB1": {
                        "id": "047Hbgu7JmwDEeqFuXq//Q=="
                    },
                    "doyId": {
                        "id": "bXS36x7gfMJVrdFwh0hNrg=="
                    },
                    "efoId": {
                        "id": "Iw+H52J9KNTxmT/GRBgcSw=="
                    },
                    "lkpenIdA": {
                        "id": "8QM7lFNZ9FKoQ8ukjdCFzA=="
                    },
                    "lkpenIdB1": {
                        "id": "8QM7lFNZ9FKoQ8ukjdCFzA=="
                    },
                    "lkpenIdB2": {
                        "id": "8QM7lFNZ9FKoQ8ukjdCFzA=="
                    },
                    "lkkoiIdB2": {
                        "id": "047Hbgu7JmwDEeqFuXq//Q=="
                    },
                    "daokKodikos": {
                        "kodikos": "EoWHUsY6N/biOzW7pPm+Aw=="
                    },
                    "opdId": {
                        "id": "WuzMVOxRhelo8bsXch2Qwg=="
                    },
                    "ddsId": {
                        "id": "Q+miKtIOtZZDH9VJa9Q5Ug=="
                    },
                    "ddrId": {
                        "id": "YQZshL1w5CJDVzyTeSQedA=="
                    },
                    "lkprfId": {
                        "id": "xoaTOHC7dea7wsFLV5rsjg=="
                    },
                    "lkprfIdB2": {
                        "id": "xoaTOHC7dea7wsFLV5rsjg=="
                    },
                    "ownerSexId": {
                        "id": "99gZmMPS9BTTkHuUFInwyw=="
                    },
                    "sexId": {
                        "id": "99gZmMPS9BTTkHuUFInwyw=="
                    },
                    "sfflagFinal": null,
                    "lastEdaKodikos": 0,
                    "maxEdaaKodikos": 1,
                    "isCrmEnabled": null,
                    "isEdeLfaFlag": 2,
                    "gusername": "ΒΑΒΑΛΟΥ ΑΡΤΕΜΗΣΙΑ",
                    "mmzCalcValue": null,
                    "efoDescription": "ONLINE_TAXIS_USERS",
                    "keaName": "ONLINE_TAXIS_USERS"
                }
            }
        ]
    }
}
```

## δικαιολογητικά
Τέλος, κάνουμε ένα αίτημα να δούμε πόσα δικαιολογητικά υπάρχουν:
curl 'https://eae2024.opekepe.gov.gr/eae2024/rest/Edetedeaeedikaiol/findAllByCriteriaRange_EdetedeaeedikaiolGrpEdl_count' \
  -H 'accept: application/json, text/plain, */*' \
  -H 'accept-language: en-US,en;q=0.8' \
  -H 'cache-control: no-cache' \
  -H 'content-type: application/json' \
  -b 'eae2024-session-id=e2cdb26e-c8dc-456d-be5e-672d39fcf15c; eae2024-subs-code="mgm/lI1McsHlNZAQL4pXeE5h9sKGQleSBIiJgqSucCs="' \
  -H 'origin: https://eae2024.opekepe.gov.gr' \
  -H 'pragma: no-cache' \
  -H 'priority: u=1, i' \
  -H 'referer: https://eae2024.opekepe.gov.gr/eae2024/' \
  -H 'sec-ch-ua: "Brave";v="137", "Chromium";v="137", "Not/A)Brand";v="24"' \
  -H 'sec-ch-ua-mobile: ?0' \
  -H 'sec-ch-ua-platform: "Windows"' \
  -H 'sec-fetch-dest: empty' \
  -H 'sec-fetch-mode: cors' \
  -H 'sec-fetch-site: same-origin' \
  -H 'sec-gpc: 1' \
  -H 'user-agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/137.0.0.0 Safari/537.36' \
  --data-raw '{"g_Ede_id":"qB8ujfgfAKWoOF+W1gH/Ow==","gParams_yearEae":2025,"exc_Id":[]}'

απάντηση:
```json
{
    "count": 1,
    "data": []
}
```

εδώ ας πούμε υπάρχει ένα. Προσθέτουμε λοιπόν επιπλέον:
1) δικαιολογητικό ταυτοπροσωπίας με κωδικό 166
2) ΑΝ υπάρχει θετική παράμετρος για συνεδεδεμένη σκληρού σίτου, βάζουμε δικαιολογητικά για καρτελες σιτου και τιμολογιο σιτου
3) ΑΝ υπάρχει θετική παράμετρος για συνεδεδεμένη μαλακου σίτου, βάζουμε δικαιολογητικά για καρτελες μαλακου σιτου και τιμολογιο μαλακου σιτου
4) ΑΝ υπάρχει θετικη παραμετρος για βαμβακι, επίσης το ίδιο
5) ΑΝ υπάρχει θετική παραμετρος για λιπάσματα βάζουμε το δικαιολογητικό με κωδικό 215 για λιπάσματα
6) ΑΝ υπάρχει θετική παράμετρος για ακροφύσια, βάζουμε και το δικαιολογητικό για τα ακροφύσια
Εγώ τα προσθέτω όλα εδώ στο παράδειγμα για να δεις πως μπαίνουν.

αίτημα:
url: https://eae2024.opekepe.gov.gr/eae2024/rest/MainService/synchronizeChangesWithDb_Edetedeaeedikaiol
method: POST
requst body:
```json
{
    "params": {
        "data": [
            {
                "status": 0,
                "when": 1750187390394,
                "entityName": "Edetedeaeedikaiol",
                "entity": {
                    "id": "TEMP_ID_35",
                    "afm": "043409376",
                    "recordtype": 0,
                    "usrinsert": null,
                    "dteinsert": null,
                    "usrupdate": null,
                    "dteupdate": null,
                    "kodikos": 10,
                    "remarks": null,
                    "ebbId": null,
                    "sexId": null,
                    "rowVersion": null,
                    "fileCode": null,
                    "fileName": null,
                    "fileHash": null,
                    "fileUrl": null,
                    "fileAttach": null,
                    "fileYear": 2025,
                    "etos": 2025,
                    "edeId": {
                        "id": "qB8ujfgfAKWoOF+W1gH/Ow=="
                    },
                    "edkId": {
                        "id": "bg7ijd2umwp6fMGcfg3ziA=="
                    }
                }
            },
            {
                "status": 0,
                "when": 1750187387242,
                "entityName": "Edetedeaeedikaiol",
                "entity": {
                    "id": "TEMP_ID_34",
                    "afm": "043409376",
                    "recordtype": 0,
                    "usrinsert": null,
                    "dteinsert": null,
                    "usrupdate": null,
                    "dteupdate": null,
                    "kodikos": 9,
                    "remarks": null,
                    "ebbId": null,
                    "sexId": null,
                    "rowVersion": null,
                    "fileCode": null,
                    "fileName": null,
                    "fileHash": null,
                    "fileUrl": null,
                    "fileAttach": null,
                    "fileYear": 2025,
                    "etos": 2025,
                    "edeId": {
                        "id": "qB8ujfgfAKWoOF+W1gH/Ow=="
                    },
                    "edkId": {
                        "id": "LeTo1TqFJQmrGUNIUb4iPA=="
                    }
                }
            },
            {
                "status": 0,
                "when": 1750187382827,
                "entityName": "Edetedeaeedikaiol",
                "entity": {
                    "id": "TEMP_ID_33",
                    "afm": "043409376",
                    "recordtype": 0,
                    "usrinsert": null,
                    "dteinsert": null,
                    "usrupdate": null,
                    "dteupdate": null,
                    "kodikos": 8,
                    "remarks": null,
                    "ebbId": null,
                    "sexId": null,
                    "rowVersion": null,
                    "fileCode": null,
                    "fileName": null,
                    "fileHash": null,
                    "fileUrl": null,
                    "fileAttach": null,
                    "fileYear": 2025,
                    "etos": 2025,
                    "edeId": {
                        "id": "qB8ujfgfAKWoOF+W1gH/Ow=="
                    },
                    "edkId": {
                        "id": "DRvwyxmdjYpP6pztWL2S8Q=="
                    }
                }
            },
            {
                "status": 0,
                "when": 1750187380260,
                "entityName": "Edetedeaeedikaiol",
                "entity": {
                    "id": "TEMP_ID_32",
                    "afm": "043409376",
                    "recordtype": 0,
                    "usrinsert": null,
                    "dteinsert": null,
                    "usrupdate": null,
                    "dteupdate": null,
                    "kodikos": 7,
                    "remarks": null,
                    "ebbId": null,
                    "sexId": null,
                    "rowVersion": null,
                    "fileCode": null,
                    "fileName": null,
                    "fileHash": null,
                    "fileUrl": null,
                    "fileAttach": null,
                    "fileYear": 2025,
                    "etos": 2025,
                    "edeId": {
                        "id": "qB8ujfgfAKWoOF+W1gH/Ow=="
                    },
                    "edkId": {
                        "id": "uMnQ+pmu2sxPxxVN0WVlNQ=="
                    }
                }
            },
            {
                "status": 0,
                "when": 1750187377817,
                "entityName": "Edetedeaeedikaiol",
                "entity": {
                    "id": "TEMP_ID_31",
                    "afm": "043409376",
                    "recordtype": 0,
                    "usrinsert": null,
                    "dteinsert": null,
                    "usrupdate": null,
                    "dteupdate": null,
                    "kodikos": 6,
                    "remarks": null,
                    "ebbId": null,
                    "sexId": null,
                    "rowVersion": null,
                    "fileCode": null,
                    "fileName": null,
                    "fileHash": null,
                    "fileUrl": null,
                    "fileAttach": null,
                    "fileYear": 2025,
                    "etos": 2025,
                    "edeId": {
                        "id": "qB8ujfgfAKWoOF+W1gH/Ow=="
                    },
                    "edkId": {
                        "id": "Wi19dzZG2iOt8IXxFdUJlg=="
                    }
                }
            },
            {
                "status": 0,
                "when": 1750187374626,
                "entityName": "Edetedeaeedikaiol",
                "entity": {
                    "id": "TEMP_ID_30",
                    "afm": "043409376",
                    "recordtype": 0,
                    "usrinsert": null,
                    "dteinsert": null,
                    "usrupdate": null,
                    "dteupdate": null,
                    "kodikos": 5,
                    "remarks": null,
                    "ebbId": null,
                    "sexId": null,
                    "rowVersion": null,
                    "fileCode": null,
                    "fileName": null,
                    "fileHash": null,
                    "fileUrl": null,
                    "fileAttach": null,
                    "fileYear": 2025,
                    "etos": 2025,
                    "edeId": {
                        "id": "qB8ujfgfAKWoOF+W1gH/Ow=="
                    },
                    "edkId": {
                        "id": "UY4OQAw5jGRyp/pz1LZVZA=="
                    }
                }
            },
            {
                "status": 0,
                "when": 1750187372115,
                "entityName": "Edetedeaeedikaiol",
                "entity": {
                    "id": "TEMP_ID_29",
                    "afm": "043409376",
                    "recordtype": 0,
                    "usrinsert": null,
                    "dteinsert": null,
                    "usrupdate": null,
                    "dteupdate": null,
                    "kodikos": 4,
                    "remarks": null,
                    "ebbId": null,
                    "sexId": null,
                    "rowVersion": null,
                    "fileCode": null,
                    "fileName": null,
                    "fileHash": null,
                    "fileUrl": null,
                    "fileAttach": null,
                    "fileYear": 2025,
                    "etos": 2025,
                    "edeId": {
                        "id": "qB8ujfgfAKWoOF+W1gH/Ow=="
                    },
                    "edkId": {
                        "id": "Il95dg/Ibi1rCO7Uf/v90A=="
                    }
                }
            },
            {
                "status": 0,
                "when": 1750187253402,
                "entityName": "Edetedeaeedikaiol",
                "entity": {
                    "id": "TEMP_ID_28",
                    "afm": "043409376",
                    "recordtype": 0,
                    "usrinsert": null,
                    "dteinsert": null,
                    "usrupdate": null,
                    "dteupdate": null,
                    "kodikos": 3,
                    "remarks": null,
                    "ebbId": null,
                    "sexId": null,
                    "rowVersion": null,
                    "fileCode": null,
                    "fileName": null,
                    "fileHash": null,
                    "fileUrl": null,
                    "fileAttach": null,
                    "fileYear": 2025,
                    "etos": 2025,
                    "edeId": {
                        "id": "qB8ujfgfAKWoOF+W1gH/Ow=="
                    },
                    "edkId": {
                        "id": "Zu50wPtrta9nV1CJTP3nkQ=="
                    }
                }
            },
            {
                "status": 0,
                "when": 1750187250669,
                "entityName": "Edetedeaeedikaiol",
                "entity": {
                    "id": "TEMP_ID_27",
                    "afm": "043409376",
                    "recordtype": 0,
                    "usrinsert": null,
                    "dteinsert": null,
                    "usrupdate": null,
                    "dteupdate": null,
                    "kodikos": 2,
                    "remarks": null,
                    "ebbId": null,
                    "sexId": null,
                    "rowVersion": null,
                    "fileCode": null,
                    "fileName": null,
                    "fileHash": null,
                    "fileUrl": null,
                    "fileAttach": null,
                    "fileYear": 2025,
                    "etos": 2025,
                    "edeId": {
                        "id": "qB8ujfgfAKWoOF+W1gH/Ow=="
                    },
                    "edkId": {
                        "id": "dJYbV47UtYLqMWj+1mas1A=="
                    }
                }
            },
            {
                "status": 1,
                "when": 0,
                "entityName": "Edetedeaeehd",
                "entity": {
                    "id": "qB8ujfgfAKWoOF+W1gH/Ow==",
                    "cuhId": null,
                    "afm": "043409376",
                    "recordtype": 0,
                    "usrinsert": "app_prod_eae2327",
                    "dteinsert": "2025-06-03T21:00:00.000Z",
                    "usrupdate": "app_prod_eae2327",
                    "dteupdate": "2025-06-16T21:00:00.000Z",
                    "dtedelete": null,
                    "prosopotype": 1,
                    "name": null,
                    "lastname": "ΑΣΦ",
                    "firstname": "ΑΣΦΞΚ",
                    "fathername": null,
                    "odosB1": null,
                    "numodosB1": null,
                    "taxkodikosB1": "68300",
                    "phone1B1": null,
                    "mobilephoneB1": "6946571234",
                    "idtype": null,
                    "idno": null,
                    "kodikos": 6311,
                    "dteprotocol": null,
                    "protocolarith": null,
                    "gusrId": 1835589,
                    "etos": 2025,
                    "invalidrecordtype": 0,
                    "remarks01": null,
                    "remarks02": null,
                    "remarks03": null,
                    "email": "ava@gmail.com",
                    "odosB2": null,
                    "numodosB2": null,
                    "taxkodikosB2": "68300",
                    "topothesiaB2": null,
                    "phone1B2": null,
                    "iban": null,
                    "ama": null,
                    "amoga": null,
                    "remarks": null,
                    "bnkAccount": null,
                    "remoteId": null,
                    "remoteEfoId": null,
                    "seiratype": 1,
                    "dtebirth": "1976-06-05T21:00:00.000Z",
                    "enoId": null,
                    "arbibl": null,
                    "remoteEdeId": null,
                    "remoteEdeEfoId": null,
                    "rejectFlag": null,
                    "etosenteea": null,
                    "p18qty": null,
                    "sefoId": null,
                    "downloadFlag": null,
                    "amka": null,
                    "entolheispflag": 1,
                    "entolhxreflag": 0,
                    "arkartaspolith": null,
                    "mcoflag": 0,
                    "genderflag": 2,
                    "asfalishnumber": null,
                    "dteasfalish": null,
                    "metanastisflag": 0,
                    "drasthriothtaflag": 0,
                    "misthotisflag": 0,
                    "ekmflag": 1,
                    "dtestartekm": null,
                    "arekm": null,
                    "eidosekmtype": null,
                    "fax": null,
                    "eprotocolno": null,
                    "asfaxiafytikovaluepro": 0,
                    "asfaxiafytikovalue": 0,
                    "asfaxiazoikovaluepro": 0,
                    "asfaxiazoikovalue": 0,
                    "eisforafytikovalue": 0,
                    "eisforazoikovalue": 0,
                    "eisfora1value": 0,
                    "asfpercentchange": 0,
                    "recordoltype": 0,
                    "usrolId": null,
                    "pendingelgaflag": 1,
                    "dtedraststart": null,
                    "dteonlineproseas": null,
                    "rowVersion": 331,
                    "prevyearid": null,
                    "troposplhromhs": null,
                    "troposypolxre": null,
                    "exoterikoSynergioFlag": 0,
                    "dtebirthvarchar": "06/06/1976",
                    "gusrIdDik": null,
                    "lastnameb": null,
                    "sfflag": null,
                    "sfapentaxhflag": null,
                    "mobilephoneCountryCodeB1": 30,
                    "egfkatflag": null,
                    "bibliatype": null,
                    "sfentaxhflag": null,
                    "newflag": null,
                    "youngflag": null,
                    "ekmfirstyear": null,
                    "eisforafytikovaluepro": 0,
                    "eisforazoikovaluepro": 0,
                    "nometabolesflag": null,
                    "tritoprosopoflag": null,
                    "allonpflag": null,
                    "polithseeflag": null,
                    "educationleveltype": null,
                    "dteOris": null,
                    "workAccessType": null,
                    "mobilephoneCountryCodeB2": 30,
                    "mobilephoneB2": null,
                    "mothername": null,
                    "daEtosPrevSum": null,
                    "daEtosPrevEde": null,
                    "daLtDaPrevFlag": null,
                    "daLtDaPrevLhxh": null,
                    "daLtDaPrevPolhsh": null,
                    "businessGroupFlag": 0,
                    "kgpk7type": null,
                    "lkkoiIdB1": {
                        "id": "047Hbgu7JmwDEeqFuXq//Q=="
                    },
                    "doyId": {
                        "id": "bXS36x7gfMJVrdFwh0hNrg=="
                    },
                    "efoId": {
                        "id": "Iw+H52J9KNTxmT/GRBgcSw=="
                    },
                    "lkpenIdA": {
                        "id": "8QM7lFNZ9FKoQ8ukjdCFzA=="
                    },
                    "lkpenIdB1": {
                        "id": "8QM7lFNZ9FKoQ8ukjdCFzA=="
                    },
                    "lkpenIdB2": {
                        "id": "8QM7lFNZ9FKoQ8ukjdCFzA=="
                    },
                    "lkkoiIdB2": {
                        "id": "047Hbgu7JmwDEeqFuXq//Q=="
                    },
                    "daokKodikos": {
                        "kodikos": "EoWHUsY6N/biOzW7pPm+Aw=="
                    },
                    "opdId": {
                        "id": "WuzMVOxRhelo8bsXch2Qwg=="
                    },
                    "ddsId": {
                        "id": "Q+miKtIOtZZDH9VJa9Q5Ug=="
                    },
                    "ddrId": {
                        "id": "YQZshL1w5CJDVzyTeSQedA=="
                    },
                    "lkprfId": {
                        "id": "xoaTOHC7dea7wsFLV5rsjg=="
                    },
                    "lkprfIdB2": {
                        "id": "xoaTOHC7dea7wsFLV5rsjg=="
                    },
                    "ownerSexId": {
                        "id": "99gZmMPS9BTTkHuUFInwyw=="
                    },
                    "sexId": {
                        "id": "99gZmMPS9BTTkHuUFInwyw=="
                    },
                    "sfflagFinal": null,
                    "lastEdaKodikos": 0,
                    "maxEdaaKodikos": 1,
                    "isCrmEnabled": null,
                    "isEdeLfaFlag": 2,
                    "gusername": "ΒΑΒΑΛΟΥ ΑΡΤΕΜΗΣΙΑ",
                    "mmzCalcValue": null,
                    "efoDescription": "ONLINE_TAXIS_USERS",
                    "keaName": "ONLINE_TAXIS_USERS"
                }
            }
        ]
    }
}
```



response:
```
{
    "newEntitiesIds": [
        {
            "entityName": "Edetedeaeedikaiol",
            "tempId": "TEMP_ID_33",
            "databaseId": "Xhhm1m76JClbmn5/ODtrRg=="
        },
        {
            "entityName": "Edetedeaeedikaiol",
            "tempId": "TEMP_ID_32",
            "databaseId": "gQvYD2PDgZ4zwIJo9Y0Y7A=="
        },
        {
            "entityName": "Edetedeaeedikaiol",
            "tempId": "TEMP_ID_35",
            "databaseId": "r805Cqw0UMnpWFPOauEq1Q=="
        },
        {
            "entityName": "Edetedeaeedikaiol",
            "tempId": "TEMP_ID_34",
            "databaseId": "rxXtHxXc7xK1vdk4u6Zj8Q=="
        },
        {
            "entityName": "Edetedeaeedikaiol",
            "tempId": "TEMP_ID_28",
            "databaseId": "Hyzhv0Nh5yqHQ5TbJjpkCg=="
        },
        {
            "entityName": "Edetedeaeedikaiol",
            "tempId": "TEMP_ID_27",
            "databaseId": "tpm69KK1kMwXs+gI5tpAYw=="
        },
        {
            "entityName": "Edetedeaeedikaiol",
            "tempId": "TEMP_ID_29",
            "databaseId": "lc/DiXP+2Bm9dGDn7B4wOw=="
        },
        {
            "entityName": "Edetedeaeedikaiol",
            "tempId": "TEMP_ID_31",
            "databaseId": "VrIz2pjq/oex/J3+paWbVQ=="
        },
        {
            "entityName": "Edetedeaeedikaiol",
            "tempId": "TEMP_ID_30",
            "databaseId": "OdMqnKerchO57p3sqhLKeA=="
        }
    ],
    "warningMessages": null,
    "infoMessages": null
}
```


Βασίσου στις συναρτήσεις εδώ:
```js
export const EAE_YEAR = 2025;

/**
 * Performs a fetch request to the specified API endpoint.
 * @param endpoint - The API endpoint to call.
 * @param body - The request payload.
 * @returns The JSON response from the API.
 */
export const fetchApi = async (endpoint: string, body: any): Promise<any> => {
    const url = `https://eae2024.opekepe.gov.gr/eae2024/rest/${endpoint}`;
    try {
        const response = await fetch(url, {
            method: 'POST',
            headers: {
                'Content-Type': 'application/json',
                'Accept': 'application/json, text/plain, */*'
            },
            credentials: 'include',
            body: JSON.stringify(body)
        });
        if (!response.ok) {
            let errorText = await response.text();
            try {
                const errorJson = JSON.parse(errorText);
                errorText = errorJson.message || errorText;
            } catch (e) { /* Ignore */ }
            throw new Error(`API Error ${response.status}: ${errorText}`);
        }
        return await response.json();
    } catch (error) {
        console.error(`Fetch failed for ${endpoint}:`, error);
        throw error;
    }
};

/**
 * Prepares an entity object for an API request by cleaning it and converting dates.
 * @param entity - The entity object to prepare.
 * @returns The prepared entity.
 */
export const prepareEntityForRequest = (entity: any): any => {
    if (!entity) return null;
    const preparedEntity = JSON.parse(JSON.stringify(entity));
    const dateKeys = ['dteinsert', 'dteupdate', 'dtebirth', 'dtedke', 'dteprotocol', 'dtestartekm', 'dteasfalish', 'dtedraststart', 'dteonlineproseas', 'dteOris'];

    function traverseAndPrepare(obj: any): any {
        if (obj === null || typeof obj !== 'object') return obj;
        if (Array.isArray(obj)) return obj.map(item => traverseAndPrepare(item));

        delete obj.$entityName;
        delete obj.$refId;

        const newObj: { [key: string]: any } = {};
        for (const key in obj) {
            if (Object.prototype.hasOwnProperty.call(obj, key)) {
                let value = obj[key];
                if (dateKeys.includes(key) && typeof value === 'number') {
                    value = new Date(value).toISOString();
                }
                if (value && typeof value === 'object' && !Array.isArray(value)) {
                    if (value.id !== undefined && value.id !== null) {
                        value = { id: value.id };
                    } else if (value.kodikos !== undefined && value.kodikos !== null && Object.keys(value).length <= 5) {
                        value = { kodikos: value.kodikos };
                    } else {
                        value = traverseAndPrepare(value);
                    }
                } else if (value && typeof value === 'object' && Array.isArray(value)) {
                    value = traverseAndPrepare(value);
                }
                if (value !== null && value !== undefined) {
                    if (typeof value !== 'object' || Array.isArray(value) || Object.keys(value).length > 0) {
                        newObj[key] = value;
                    }
                }
            }
        }
        return newObj;
    }
    return traverseAndPrepare(preparedEntity);
};

/**
 * Sends a batch of changes to the backend for synchronization.
 * @param dataArray - The array of change objects.
 * @returns The API response.
 */
export const synchronizeChanges = async (dataArray: any[]): Promise<any> => {
    const preparedDataArray = dataArray.map(change => ({
        ...change,
        entity: prepareEntityForRequest(change.entity)
    }));
    return fetchApi('MainService/synchronizeChangesWithDb_Edetedeaeeagroi', {
        params: { data: preparedDataArray }
    });
};

/**
 * A wrapper for synchronizeChanges that also handles fetching the main application header (Edehd)
 * and adding it to the list of changes, which is required for most sync operations.
 * @param changes - The array of changes to execute (without the Edehd).
 * @param mainApplicationId - The ID of the main application.
 * @returns The result of the synchronizeChanges call.
 */
export const executeSync = async (changes: any[], mainApplicationId: string): Promise<any> => {
    if (!mainApplicationId) {
        throw new Error("Main Application ID is required for executeSync.");
    }
    if (changes.length === 0) {
        console.warn("executeSync called with no changes.");
        return;
    }

    const edehdResponse = await fetchApi('Edetedeaeehd/findById', { id: mainApplicationId });
    const currentEdehd = edehdResponse.data[0];

    const updatedEdehd = {
        ...currentEdehd,
        rowVersion: currentEdehd.rowVersion + 2
    };

    const finalChanges = changes.map(change => ({
        ...change,
        when: change.when || Date.now(),
    }));

    finalChanges.push({
        status: 1, // Update
        when: 0,
        entityName: "Edetedeaeehd",
        entity: updatedEdehd
    });

    return synchronizeChanges(finalChanges);
}; 
```


δες και ένα παράδειγμα με αγροτεμάχια εδώ:
```js
import {
    fetchApi,
    synchronizeChanges,
    executeSync,
    EAE_YEAR
} from '../utils/api_helpers';

/**
 * Copies crop, cultivation, and eco-scheme data from a source parcel to multiple target parcels.
 * @param mainApplicationId - The main application ID (edeId).
 */
export async function copyAgrotemaxioData(mainApplicationId: string) {
    if (!mainApplicationId) {
        alert("ID Αίτησης δεν έχει οριστεί. Ανανεώστε τη σελίδα πάνω σε μια αίτηση.");
        return;
    }

    try {
        // --- 0. Επιβεβαίωση Χρήστη ---
        const edehdResponse = await fetchApi('Edetedeaeehd/findById', { id: mainApplicationId });
        const currentEdehd = edehdResponse.data[0];
        const confirmMessage = `Ενέργεια: Αντιγραφή Καλλιεργειών & Οικολογικών Σχημάτων\n\nΑίτηση:\nAFM: ${currentEdehd.afm}\nΌνομα: ${currentEdehd.firstname}\nΕπώνυμο: ${currentEdehd.lastname}\n\nΠατήστε ΟΚ για να συνεχίσετε.`;
        if (!window.confirm(confirmMessage)) {
            alert("Η διαδικασία ακυρώθηκε από τον χρήστη.");
            return;
        }

        //αποθήκευση κωδικών που είχαν σφάλματα
        const errors = [];
        // --- 1. Λήψη όλων των αγροτεμαχίων ---
        console.log("Fetching all agrotemaxia...");
        const allAgrotemaxiaResponse = await fetchApi('Edetedeaeeagroi/findAllByCriteriaRange_EdetedeaeeagroiGrpEda', { g_Ede_id: mainApplicationId, gParams_yearEae: EAE_YEAR, fromRowIndex: 0, toRowIndex: 1000 });
        const agrotemaxiaMap = new Map(allAgrotemaxiaResponse.data.map((agro: any) => [String(agro.kodikos), agro]));
        const availableKodikoi = Array.from(agrotemaxiaMap.keys()).join(', ');
        console.log(`Available agrotemaxio kodikoi: ${availableKodikoi}`);

        // --- 2. Είσοδος Πηγής και Στόχων ---
        const sourceKodikos = prompt(`Εισάγετε τον ΚΩΔΙΚΟ του αγροτεμαχίου-ΠΗΓΗΣ.\nΔιαθέσιμοι: ${availableKodikoi}`);
        if (!sourceKodikos || !agrotemaxiaMap.has(sourceKodikos)) {
            alert(`Σφάλμα: το αγροτεμάχιο-πηγή με κωδικό '${sourceKodikos}' δεν βρέθηκε.`);
            return;
        }
        const sourceAgrotemaxio: any = agrotemaxiaMap.get(sourceKodikos);

        const targetKodikoiInput = prompt(`Εισάγετε τους ΚΩΔΙΚΟΥΣ των αγροτεμαχίων-ΣΤΟΧΩΝ, χωρισμένους με κόμμα (π.χ. 2, 3, 4):`);
        if (!targetKodikoiInput) {
            alert("Σφάλμα: Δεν δόθηκαν αγροτεμάχια-στόχοι.");
            return;
        }
        const targetKodikoi = targetKodikoiInput.replaceAll(";", ",").split(',').map(k => k.trim()).filter(k => k);

        // --- 3. Ανάκτηση ΟΛΩΝ των Δεδομένων Πηγής ---
        console.log(`Fetching ALL data from source agrotemaxio (kodikos: ${sourceKodikos})...`);
        const sourceFytikoResponse = await fetchApi('Edetedeaeefytiko/findAllByCriteriaRange_EdetedeaeeagroiGrpEdf', { edaId_id: sourceAgrotemaxio.id, gParams_yearEae: EAE_YEAR, fromRowIndex: 0, toRowIndex: 10 });
        const sourceFytiko = (sourceFytikoResponse.data && sourceFytikoResponse.data.length > 0) ? sourceFytikoResponse.data[0] : null;

        let sourceSyndedemeni = null;
        if (sourceFytiko) {
            const sourceSyndedemeniResponse = await fetchApi('Edetedeaeerequestfytiko/findAllByCriteriaRange_EdetedeaeeagroiGrpEfrq', { edfId_id: sourceFytiko.id, gParams_yearEae: EAE_YEAR, fromRowIndex: 0, toRowIndex: 10 });
            sourceSyndedemeni = (sourceSyndedemeniResponse.data && sourceSyndedemeniResponse.data.length > 0) ? sourceSyndedemeniResponse.data[0] : null;
        }

        const sourceEcoSchemesResponse = await fetchApi('Edetedeaeeagroieco/findAllByCriteriaRange_EdetedeaeeagroiGrpEdaec', { edaId_id: sourceAgrotemaxio.id, fromRowIndex: 0, toRowIndex: 500 });
        const sourceEcoSchemes = sourceEcoSchemesResponse.data || [];
        console.log(`Source has ${sourceEcoSchemes.length} eco-schemes.`);

        // --- 4. Loop για κάθε Στόχο ---
        console.log("--- Starting Copy Process ---");
        for (const targetKodikos of targetKodikoi) {
            console.log(`\n--- Processing Target Kodikos: ${targetKodikos} ---`);
            if (!agrotemaxiaMap.has(targetKodikos) || sourceKodikos === targetKodikos) {
                console.error(`Invalid or same-as-source target kodikos '${targetKodikos}'. Skipping.`);
                continue;
            }
            const targetAgrotemaxio: any = agrotemaxiaMap.get(targetKodikos);

            try {
                // ΕΠΕΞΕΡΓΑΣΙΑ ΚΑΛΛΙΕΡΓΕΙΑΣ & ΣΥΝΔΕΔΕΜΕΝΗΣ
                if (sourceFytiko) {
                    console.log(`Processing Kalliergia/Syndedemeni for target ${targetKodikos}...`);
                    const targetFytikoResponse = await fetchApi('Edetedeaeefytiko/findAllByCriteriaRange_EdetedeaeeagroiGrpEdf', { edaId_id: targetAgrotemaxio.id, gParams_yearEae: EAE_YEAR, fromRowIndex: 0, toRowIndex: 10 });
                    const targetFytiko = (targetFytikoResponse.data && targetFytikoResponse.data.length > 0) ? targetFytikoResponse.data[0] : null;

                    if (targetFytiko) {
                        const changes = [];

                        // ΒΗΜΑ 5.1: Έλεγχος και προετοιμασία διαγραφής παλιάς συνδεδεμένης του TARGET
                        const targetSyndedemenes = await fetchApi('Edetedeaeerequestfytiko/findAllByCriteriaRange_EdetedeaeeagroiGrpEfrq', { edfId_id: targetFytiko.id, gParams_yearEae: EAE_YEAR, fromRowIndex: 0, toRowIndex: 10 });
                        if (targetSyndedemenes.data && targetSyndedemenes.data.length > 0) {
                            console.log(`Target ${targetKodikos} has existing syndedemenes. They will be deleted.`);
                            for (const synd of targetSyndedemenes.data) {
                                changes.push({
                                    status: 2, // Delete
                                    when: Date.now(),
                                    entityName: "Edetedeaeerequestfytiko",
                                    entity: { id: synd.id, rowVersion: synd.rowVersion }
                                });
                            }
                        }

                        // ΒΗΜΑ 5.2: Προετοιμασία Ανανέωσης του Φυτικού Κεφαλαίου του TARGET
                        const updatedFytikoEntity = {
                            ...targetFytiko,
                                      efyId: { id: sourceFytiko.efyId.id },
        poiId: { id: sourceFytiko.poiId.id },
        emxpId: sourceFytiko.emxpId ? { id: sourceFytiko.emxpId.id } : null,
        emccId: sourceFytiko.emccId ? { id: sourceFytiko.emccId.id } : null,
        efecId: sourceFytiko.efecId ? { id: sourceFytiko.efecId.id } : null,
                        };
                        changes.push({
                            status: 1, // Update
                            when: Date.now(),
                            entityName: "Edetedeaeefytiko",
                            entity: updatedFytikoEntity
                        });

                        // ΒΗΜΑ 5.3: Προετοιμασία Προσθήκης ΝΕΑΣ Συνδεδεμένης (αν υπάρχει στην πηγή)
                        if (sourceSyndedemeni && sourceSyndedemeni.eschId && sourceSyndedemeni.eschId.id) {
                            const edehdResponseForSexId = await fetchApi('Edetedeaeehd/findById', { id: mainApplicationId });
                            const userSexId = edehdResponseForSexId.data[0].sexId.id || edehdResponseForSexId.data[0].sexId.$refId;

                            if (!userSexId) throw new Error("Could not determine user's Subscriber ID.");

                            const newRequestFytikoEntity = {
                                id: `TEMP_ID_${Date.now()}`,
                                afm: sourceAgrotemaxio.afm,
                                kodikos: 1, // Ξεκινάμε από 1 αφού διαγράψαμε τις παλιές
                                etos: EAE_YEAR,
                                edeId: { id: mainApplicationId },
                                edaId: { id: targetAgrotemaxio.id },
                                edfId: { id: targetFytiko.id }, // Σύνδεση με το fytiko του target
                                efyId: { id: sourceFytiko.efyId.id },
                                poiId: { id: sourceFytiko.poiId.id },
                                eschId: { id: sourceSyndedemeni.eschId.id },
                                sexId: { id: userSexId },
                                // Τα υπόλοιπα πεδία θα είναι null ή default
                                recordtype: 0, eschLt2: 2, rowVersion: null,
                                usrinsert: null, dteinsert: null, usrupdate: null, dteupdate: null,
                            };
                            changes.push({
                                status: 0, // Create
                                when: Date.now(),
                                entityName: "Edetedeaeerequestfytiko",
                                entity: newRequestFytikoEntity
                            });
                        } else {
                            console.log("Source agrotemaxio has no syndedemeni to copy.");
                        }

                        // ΒΗΜΑ 5.4: Προετοιμασία του Edetedeaeehd
                        const edehdResponse = await fetchApi('Edetedeaeehd/findById', { id: mainApplicationId });
                        const currentEdehd = edehdResponse.data[0];
                        changes.push({
                            status: 1,
                            when: 0,
                            entityName: "Edetedeaeehd",
                            entity: { ...currentEdehd, rowVersion: currentEdehd.rowVersion + 2 }
                        });

                        // ΒΗΜΑ 5.5: Αποστολή του ενιαίου batch
                        console.log(`Sending combined Delete/Update/Create request for target ${targetKodikos}...`);
                        await synchronizeChanges(changes);
                        console.log(`Kalliergia/Syndedemeni for target ${targetKodikos} processed successfully.`);

                    } else {
                        console.warn(`Target ${targetKodikos} has no fytiko to update. Skipping kalliergia copy.`);
                    }
                }

                // ΕΠΕΞΕΡΓΑΣΙΑ ΟΙΚΟΛΟΓΙΚΩΝ ΣΧΗΜΑΤΩΝ
                if (sourceEcoSchemes.length > 0) {
                    console.log(`Processing Eco-Schemes for target ${targetKodikos}...`);

                    // Έλεγχος αν το target έχει ήδη οικολογικά σχήματα. Αν ναι, τα παρακάμπτουμε.
                    const targetEcoSchemes = await fetchApi('Edetedeaeeagroieco/findAllByCriteriaRange_EdetedeaeeagroiGrpEdaec', { edaId_id: targetAgrotemaxio.id, fromRowIndex: 0, toRowIndex: 500 });
                    if (targetEcoSchemes.data && targetEcoSchemes.data.length > 0) {
                        console.warn(`Target ${targetKodikos} already has eco-schemes. Skipping eco-scheme copy to avoid duplicates.`);
                    } else {
                        // Το target είναι "καθαρό", οπότε προχωράμε στην προσθήκη
                        const ecoChanges = [];
                        let ecoKodikosCounter = 0;

                        for (const srcEco of sourceEcoSchemes) {
                            ecoKodikosCounter++;
                            const newEcoEntity = {
                                id: `TEMP_ID_ECO_${Date.now()}_${ecoKodikosCounter}`,
                                afm: sourceAgrotemaxio.afm,
                                recordtype: 0,
                                usrinsert: null, dteinsert: null, usrupdate: null, dteupdate: null,
                                kodikos: ecoKodikosCounter,
                                sexId: null, // Όπως στο επιτυχημένο request
                                rowVersion: null,
                                esruId: null,
                                datasourcetype: 2,
                                etos: EAE_YEAR,
                                edeId: { id: mainApplicationId },
                                edaId: { id: targetAgrotemaxio.id },
                                essuId: { id: srcEco.essuId.id } // Παίρνουμε το ID από την πηγή
                            };
                            ecoChanges.push({
                                status: 0,
                                when: Date.now(),
                                entityName: "Edetedeaeeagroieco",
                                entity: newEcoEntity
                            });
                        }

                        // Προσθήκη του Edetedeaeehd στο τέλος του batch
                        const edehdResponseForEco = await fetchApi('Edetedeaeehd/findById', { id: mainApplicationId });
                        const currentEdehdForEco = edehdResponseForEco.data[0];
                        ecoChanges.push({
                            status: 1,
                            when: 0,
                            entityName: "Edetedeaeehd",
                            entity: {
                                ...currentEdehdForEco,
                                rowVersion: currentEdehdForEco.rowVersion + 2
                            }
                        });

                        console.log(`Sending ${ecoChanges.length - 1} new eco-scheme(s) for target ${targetKodikos}...`);
                        await synchronizeChanges(ecoChanges);
                        console.log(`Eco-schemes for target ${targetKodikos} processed successfully.`);
                    }
                }

            } catch (error) {
                errors.push(targetKodikos);
                console.error(`Failed to process target kodikos: ${targetKodikos}. Error: ${(error as Error).message}`);
            }
        }

        alert(`Η αντιγραφή ολοκληρώθηκε. Υπάρχουν ${errors.length} σφάλματα στους στόχους: ${errors.join(', ')}`);

    } catch (error) {
        alert(`Προέκυψε κρίσιμο σφάλμα: ${(error as Error).message}`);
        console.error("Full error details:", error);
    }
}


/**
 * Copies the bioflag value from a source parcel to multiple target parcels.
 * @param mainApplicationId - The main application ID (edeId).
 */
export async function copyBioflagToTargets(mainApplicationId: string) {
    if (!mainApplicationId) {
        alert("ID Αίτησης δεν έχει οριστεί. Ανανεώστε τη σελίδα πάνω σε μια αίτηση.");
        return;
    }

    try {
        // --- 1. Λήψη Βασικών Πληροφοριών & Αγροτεμαχίων ---
        console.log("Fetching all agrotemaxia for bioflag copy...");
        const allAgrotemaxiaResponse = await fetchApi('Edetedeaeeagroi/findAllByCriteriaRange_EdetedeaeeagroiGrpEda', {
            g_Ede_id: mainApplicationId,
            gParams_yearEae: EAE_YEAR,
            fromRowIndex: 0,
            toRowIndex: 1000
        });
        const agrotemaxiaMap = new Map(allAgrotemaxiaResponse.data.map((agro: any) => [String(agro.kodikos), agro]));
        const availableKodikoi = Array.from(agrotemaxiaMap.keys()).join(', ');
        console.log(`Available agrotemaxio kodikoi: ${availableKodikoi}`);

        // --- 2. Είσοδος Πηγής και Στόχων ---
        const sourceKodikos = prompt(`Εισάγετε τον ΚΩΔΙΚΟ του αγροτεμαχίου-ΠΗΓΗΣ για το bioflag.`);
        if (!sourceKodikos || !agrotemaxiaMap.has(sourceKodikos)) {
            alert(`Σφάλμα: το αγροτεμάχιο-πηγή με κωδικό '${sourceKodikos}' δεν βρέθηκε.`);
            return;
        }
        const sourceAgrotemaxio: any = agrotemaxiaMap.get(sourceKodikos);
        const bioflagToCopy = sourceAgrotemaxio.bioflag;
        // alert(`Η τιμή του bioflag που θα αντιγραφεί από τον κωδικό ${sourceKodikos} είναι: ${bioflagToCopy}`);

        const targetKodikoiInput = prompt(`Εισάγετε τους ΚΩΔΙΚΟΥΣ των αγροτεμαχίων-ΣΤΟΧΩΝ, χωρισμένους με κόμμα:`);
        if (!targetKodikoiInput) {
            alert("Σφάλμα: Δεν δόθηκαν αγροτεμάχια-στόχοι.");
            return;
        }
        const targetKodikoi = targetKodikoiInput.split(',').map(k => k.trim()).filter(k => k);

        // --- 3. Δημιουργία του πίνακα αλλαγών (changes) ---
        const changesToExecute: any[] = [];
        for (const kodikos of targetKodikoi) {
            if (!agrotemaxiaMap.has(kodikos)) {
                console.warn(`Ο στόχος με κωδικό ${kodikos} δεν βρέθηκε. Παράβλεψη.`);
                continue;
            }
            if (kodikos === sourceKodikos) {
                console.warn(`Ο στόχος ${kodikos} είναι ίδιος με την πηγή. Παράβλεψη.`);
                continue;
            }

            const targetAgrotemaxio: any = agrotemaxiaMap.get(kodikos);
            if (targetAgrotemaxio.bioflag === bioflagToCopy) {
                console.log(`Ο στόχος ${kodikos} έχει ήδη τη σωστή τιμή bioflag (${bioflagToCopy}). Παράβλεψη.`);
                continue;
            }

            const updateEntity = {
                ...targetAgrotemaxio,
                bioflag: bioflagToCopy
            };

            changesToExecute.push({
                status: 1, // Update
                entityName: "Edetedeaeeagroi",
                entity: updateEntity
            });
        }

        // --- 4. Έλεγχος και Εκτέλεση ---
        if (changesToExecute.length === 0) {
            alert("Δεν απαιτούνται αλλαγές. Όλοι οι στόχοι είχαν ήδη τη σωστή τιμή ή ήταν άκυροι.");
            return;
        }

        // alert(`Προετοιμασία για την ενημέρωση του bioflag σε ${changesToExecute.length} αγροτεμάχια.`);
        
        const result = await executeSync(changesToExecute, mainApplicationId);

        alert("Η διαδικασία ενημέρωσης του bioflag ολοκληρώθηκε με επιτυχία!");
        console.log("Server Response:", result);

    } catch (error) {
        alert(`Προέκυψε σφάλμα κατά την αντιγραφή του bioflag: ${(error as Error).message}`);
        console.error("Full error details:", error);
    }
} 
```

Ο κώδικας που θα προστεθεί για τη συντομογραφία:
```js
case 'm': {
      if (!appId) {
        alert('ID Αίτησης δεν έχει οριστεί. Ανανεώστε τη σελίδα πάνω σε μια αίτηση.');
        break;
      }
      const input = prompt('Επικόλλησε το JSON εισόδου για μαζική ενημέρωση:');
      if (!input) break;
      let jsonInput;
      try {
        jsonInput = JSON.parse(input);
      } catch (e) {
        alert('Μη έγκυρο JSON.');
        break;
      }
      await handleMassUpdateFromJson(jsonInput, appId);
      break;
    }
```

Απλά πρέπει να φτιαχτεί η σωστή συνάρτηση handleMassUpdateFromJson τώρα με βάση αυτά πο σου περιγράφω.

Έτσι φαντάζομαι να πρέπει να είναι το json εισόδου:
```json
{
  "exisotiki": true,
  "skliros_sitos": true,
  "malakos_sitos": false,
  "vamvaki": true,
  "lipasmata": true,
  "viologiko": true,
  "akrofysia": false,
  "hlianthos_sumbasi": true,
  "timologia": [
    {
      "kalliergeia": "skliros_sitos",
      "afm": "096049221",
      "epwnymia": "ΕΝΩΣΗ ΑΓΡΟΤΙΚΩΝ ΣΥΝΕΤΑΙΡΙΣΜΩΝ ΟΡΕΣΤΙΑΔΑΣ",
      "hmerominia": "2024-12-31T22:00:00.000Z",
      "posotita": 100,
      "etiketes": 5,
      "poikilia": "MARAKAS"
    },
    {
      "kalliergeia": "malakos_sitos",
      "afm": "096049221",
      "epwnymia": "ΕΝΩΣΗ ΑΓΡΟΤΙΚΩΝ ΣΥΝΕΤΑΙΡΙΣΜΩΝ ΟΡΕΣΤΙΑΔΑΣ",
      "hmerominia": "2024-12-31T22:00:00.000Z",
      "posotita": 100,
      "etiketes": 5,
      "poikilia": "SICARIO"
    },
    {
      "kalliergeia": "vamvaki",
      "afm": "096049221",
      "epwnymia": "ΕΝΩΣΗ ΑΓΡΟΤΙΚΩΝ ΣΥΝΕΤΑΙΡΙΣΜΩΝ ΟΡΕΣΤΙΑΔΑΣ",
      "hmerominia": "2024-12-31T22:00:00.000Z",
      "posotita": 100,
      "etiketes": 5,
      "poikilia": "ZETA 2"
    }
  ]
}
```

και η ζητούμενη συνάρτηση θα ξεκινάει κάπως έτσι:
```js
async function handleMassUpdateFromJson(jsonInput: any, appId: string) {
  // 1. Fetch gdpr info
  const gdprResp = await fetchApi('MainService/refreshGdpr', { edeId: appId, etos: EAE_YEAR });

  // 2. Fetch anadian (αναδιανεμητική eligibility)
  const anadianResp = await fetchApi('Anadian/findAllByCriteriaRange_EdetedeaeehdGrpEdeAnadian', {
    edeId_id: appId,
    fromRowIndex: 0,
    toRowIndex: 10,
    exc_Id: []
  });
  const anadian = anadianResp.data && anadianResp.data.length > 0 ? anadianResp.data[0] : null;
  const isEpileximosAnadian = anadian && anadian.epileximosflag === true;

  // 3. Fetch υπάρχοντα μέτρα (Edetedeaeepaa)
  const metraResp = await fetchApi('Edetedeaeepaa/findAllByCriteriaRange_EdetedeaeehdGrpEdaa_count', {
    edeId_id: appId,
    gParams_yearEae: EAE_YEAR,
    exc_Id: []
  });
  const metraCount = metraResp.count;

  // 4. Fetch υπάρχοντα αιτήματα άμεσων ενισχύσεων (Edetedeaeerequest)
  const requestsResp = await fetchApi('Edetedeaeerequest/findAllByCriteriaRange_EdetedeaeehdGrpEdrq_count', {
    edeId_id: appId,
    gParams_yearEae: EAE_YEAR,
    exc_Id: []
  });
  const requestsCount = requestsResp.count;

  // 5. Fetch GDPR ids (Edetedeaeegdpr)
  const gdprIdsResp = await fetchApi('Edetedeaeegdpr/findAllByCriteriaRange_EdetedeaeehdGrpEdgdpr', {
    edeId_id: appId,
    gParams_yearEae: EAE_YEAR,
    fromRowIndex: 0,
    toRowIndex: 2000,
    exc_Id: []
  });
  const gdprEntities = gdprIdsResp.data || [];

  // 6. Fetch υπάρχοντα δικαιολογητικά (Edetedeaeedikaiol)
  const dikaiologitikaResp = await fetchApi('Edetedeaeedikaiol/findAllByCriteriaRange_EdetedeaeedikaiolGrpEdl_count', {
    g_Ede_id: appId,
    gParams_yearEae: EAE_YEAR,
    exc_Id: []
  });
  const dikaiologitikaCount = dikaiologitikaResp.count;
  
  //TODO: CONTINUE
```  
