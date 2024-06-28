*** Settings ***
Library    SeleniumLibrary
Library    OperatingSystem

*** Variables ***
${BROWSER}    chrome
${URL}        https://www.google.com
${HEADLESS_OPTIONS}    --headless --disable-gpu --no-sandbox --disable-dev-shm-usage

*** Test Cases ***
Verificar Título do Google
    ${options}=    Evaluate    sys.modules['selenium.webdriver'].ChromeOptions()    sys, selenium.webdriver
    Call Method    ${options}    add_argument    ${HEADLESS_OPTIONS}
    ${driver}=    Create Webdriver    Chrome    chrome_options=${options}
    Open Browser    ${URL}    browser=${BROWSER}
    ${title}=    Get Title
    Should Contain    ${title}    Google
    Log    Título verificado com sucesso: ${title}
    Close Browser
