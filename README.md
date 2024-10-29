const puppeteer = require('puppeteer');

(async () => {
    const browser = await puppeteer.launch({
        executablePath: '/usr/bin/chromium-browser', // Adjust path as necessary
        headless: false,
        args: ['--no-sandbox', '--disable-setuid-sandbox']
    });
    const page = await browser.newPage();

    await page.goto('https://1win.co.ke/login');
    await page.waitForNavigation({ waitUntil: 'networkidle0' });

    const mobileNumberInput = await page.waitForSelector('input[type="text"][placeholder="Mobile number"]', { timeout: 60000 });
    if (mobileNumberInput) {
        const mobileNumber = 'your_mobile_number';
        console.log('Mobile number is:', mobileNumber);
        await mobileNumberInput.type(mobileNumber);
        console.log('Typed mobile number successfully.');
    } else {
        console.error('Mobile number input field not found.');
    }

    await browser.close();
})();
