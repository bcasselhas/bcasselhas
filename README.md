const { Client, LocalAuth } = require('whatsapp-web.js');
const qrcode = require('qrcode-terminal');

const client = new Client({
    authStrategy: new LocalAuth()
});

client.on('qr', (qr) => {
    // Gerar o QR code para autenticar no WhatsApp Web
    qrcode.generate(qr, { small: true });
});

client.on('ready', () => {
    console.log('WhatsApp BOT está pronto!');
});

client.on('message', async msg => {
    if (msg.body.toLowerCase() === 'oi' || msg.body.toLowerCase() === 'olá') {
        const greetingMessage = 'Olá! Obrigado por entrar em contato. Como podemos ajudar você hoje?\n\n' +
            '1. Reparos de tela\n' +
            '2. Problemas com bateria\n' +
            '3. Outros problemas\n\n' +
            'Por favor, responda com o número da opção desejada.';

        msg.reply(greetingMessage);
    } else if (msg.body === '1') {
        const screenRepairMessage = 'Você selecionou "Reparos de tela". Por favor, informe o modelo do seu dispositivo para que possamos fornecer um orçamento:\n\n' +
            '1. iPhone\n' +
            '2. Samsung\n' +
            '3. Outro';

        msg.reply(screenRepairMessage);
    } else if (msg.body === '2') {
        const batteryIssuesMessage = 'Você selecionou "Problemas com bateria". Por favor, informe o modelo do seu dispositivo para que possamos fornecer um orçamento:\n\n' +
            '1. iPhone\n' +
            '2. Samsung\n' +
            '3. Outro';

        msg.reply(batteryIssuesMessage);
    } else if (msg.body === '3') {
        const otherIssuesMessage = 'Você selecionou "Outros problemas". Por favor, descreva o problema que está enfrentando ou selecione um dos modelos abaixo para mais opções:\n\n' +
            '1. iPhone\n' +
            '2. Samsung\n' +
            '3. Outro';

        msg.reply(otherIssuesMessage);
    } else if (['1', '2', '3'].includes(msg.body)) {
        const modelMessage = 'Por favor, informe o modelo específico do seu dispositivo (Ex: iPhone 12, Galaxy S21, etc.).';

        msg.reply(modelMessage);
    } else {
        msg.reply('Desculpe, não entendi sua resposta. Por favor, responda com um número correspondente à opção desejada.');
    }
});

client.initialize();
