# Session
Claro, vou lhe mostrar como criar uma sessão em PHP que redireciona para o arquivo "home.php" na pasta "adm" após o login bem-sucedido. Primeiro, você precisa criar um arquivo PHP para a página de login, por exemplo, "login.php". Vou assumir que você já possui um formulário HTML para a entrada do usuário. Aqui está um exemplo básico de como fazer isso:

```php
<?php
// Inicie a sessão
session_start();

// Verifique se o formulário foi enviado
if ($_SERVER["REQUEST_METHOD"] == "POST") {
    // Verifique as credenciais do usuário (substitua isso com sua lógica de verificação real)
    $username = "seu_usuario"; // Substitua pelo seu nome de usuário
    $password = "sua_senha";   // Substitua pela sua senha

    if ($_POST["username"] === $username && $_POST["password"] === $password) {
        // Credenciais corretas, defina uma variável de sessão para indicar o login bem-sucedido
        $_SESSION["loggedin"] = true;

        // Redirecione para a página home.php na pasta "adm"
        header("location: adm/home.php");
        exit;
    } else {
        $erro = "Credenciais inválidas";
    }
}
?>

<!DOCTYPE html>
<html>
<head>
    <title>Página de Login</title>
</head>
<body>

<h2>Login</h2>
<form method="post" action="">
    <label for="username">Nome de Usuário:</label>
    <input type="text" id="username" name="username" required><br><br>

    <label for="password">Senha:</label>
    <input type="password" id="password" name="password" required><br><br>

    <input type="submit" value="Login">
</form>

<?php
// Exibir mensagem de erro, se houver
if (isset($erro)) {
    echo "<p>$erro</p>";
}
?>

</body>
</html>
```

Neste exemplo, estamos verificando se o nome de usuário e a senha correspondem aos valores definidos nas variáveis `$username` e `$password`. Se as credenciais estiverem corretas, definimos a variável de sessão `$_SESSION["loggedin"]` como `true` e redirecionamos o usuário para a página "home.php" na pasta "adm" usando `header("location: adm/home.php")`.

Agora, você precisa criar o arquivo "home.php" na pasta "adm" com o conteúdo específico da página que deseja exibir após o login bem-sucedido.

Lembre-se de substituir os valores de `$username` e `$password` com as credenciais reais que você deseja verificar em seu sistema de login real. Além disso, é importante implementar um sistema de autenticação seguro em um ambiente de produção. Este é apenas um exemplo básico para ilustrar o conceito de sessões e redirecionamento em PHP.

Se você deseja proteger o acesso ao arquivo "home.php" e garantir que somente usuários autenticados possam acessá-lo, você pode adicionar uma verificação de sessão no início do arquivo "home.php". Aqui está como você pode fazer isso:

```php
<?php
// Inicie a sessão se ela ainda não estiver iniciada
session_start();

// Verifique se o usuário está autenticado
if (!isset($_SESSION["loggedin"]) || $_SESSION["loggedin"] !== true) {
    // Se o usuário não estiver autenticado, redirecione-o de volta para a página de login
    header("location: ../login.php");
    exit;
}

// O restante do seu código para a página "home.php" continua aqui
// ...

?>

<!DOCTYPE html>
<html>
<head>
    <title>Página Home</title>
</head>
<body>

<h2>Bem-vindo à Página Home</h2>
<p>Conteúdo da página home vai aqui.</p>

</body>
</html>
```

Neste exemplo, verificamos se a sessão `$_SESSION["loggedin"]` está definida e se o seu valor é `true`. Se não estiver, redirecionamos o usuário de volta para a página de login. Isso garante que apenas usuários autenticados possam acessar a página "home.php" na pasta "adm".

Certifique-se de que a verificação de sessão esteja no início do arquivo "home.php" antes de qualquer conteúdo da página que você deseja proteger.
