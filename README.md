# usando-java-script-pela-primeira-vez
continuação do site de ongs, javascript


meu codigo de java:

document.addEventListener('DOMContentLoaded', () => {
    // Lógica para navegação mobile
    const navToggle = document.querySelector('.nav-toggle');
    const navMenu = document.querySelector('.nav-menu');

    if (navToggle && navMenu) {
        navToggle.addEventListener('click', () => {
            const isExpanded = navToggle.getAttribute('aria-expanded') === 'true' || false;
            navToggle.setAttribute('aria-expanded', !isExpanded);
            navMenu.classList.toggle('is-open');
        });
    }

    // Lógica para validação e submissão do formulário
    const donationForm = document.querySelector('.donation-form');
    if (donationForm) {
        donationForm.addEventListener('submit', async (event) => {
            event.preventDefault(); // Impede o envio padrão do formulário

            const amount = document.getElementById('donation-amount').value;
            const email = document.getElementById('donation-email').value;

            if (!amount || !email) {
                alert('Por favor, preencha todos os campos.');
                return;
            }

            try {
                // Simulação de requisição AJAX com Fetch API
                const response = await fetch('/api/doacao', {
                    method: 'POST',
                    headers: {
                        'Content-Type': 'application/json'
                    },
                    body: JSON.stringify({ amount, email })
                });

                if (response.ok) {
                    alert('Doação recebida com sucesso! Obrigado!');
                    donationForm.reset();
                } else {
                    alert('Erro ao processar a doação. Tente novamente mais tarde.');
                }
            } catch (error) {
                console.error('Erro:', error);
                alert('Ocorreu um erro na sua solicitação. Verifique sua conexão.');
            }
        });
    }
});
