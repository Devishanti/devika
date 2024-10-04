describe('Проверка контактной информации на сайте Byndyusoft', () => {
    it('Проверяет ссылку на Telegram', () => {
        // Переход на главную страницу Google
        cy.visit('https://www.google.ru/');
        
        // Ждем 3 секунды
        cy.wait(3000);

        // Используем указанный селектор для поиска строки
        cy.get('body > div.L3eUgb > div.o3j99.ikrT4e.om7nvf > form > div:nth-child(1) > div.A8SBwf > div.RNNXgb')
            .filter(':visible')
            .first()
            .type('Byndyusoft{enter}'); 

        // Увеличиваем время ожидания для нахождения элемента h3
        cy.get('h3', { timeout: 10000 })
            .first()
            .click()
            .then(() => {
                // Логируем URL после клика
                cy.url().then((url) => {
                    cy.log(`Текущий URL: ${url}`);
                });
            });

        // Проверяем, что кнопка "Заказать презентацию" присутствует на странице
        cy.get('body > section.knowMore > div > span', { timeout: 20000 }) // Используем указанный селектор
            .should('be.visible')
            .then(($button) => {
                if ($button.length) {
                    cy.log('Кнопка "Заказать презентацию" найдена.');
                } else {
                    cy.log('Кнопка "Заказать презентацию" не найдена.');
                }
            })
            .click(); 

        // Проверяем ссылку на Telegram
        cy.get('a[href="http://t.me/alexanderbyndyu"]', { timeout: 10000 })
            .should('be.visible')
            .and('have.attr', 'href', 'http://t.me/alexanderbyndyu');
    });
});

