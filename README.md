# PyTOMLEncrypt

PyTOMLEncrypt is a Python package designed to solve the challenge of securely sharing credentials between developers, environments, containers, and GitHub repositories. It provides a simple way to encrypt and decrypt TOML configuration files containing sensitive data, allowing you to safely commit these files while retaining control over the encryption keys to be shared with developers and injected into containers as needed.

## Features

- Encrypt TOML files containing sensitive data
- Decrypt encrypted TOML files for use in your applications
- Flexible key management: use file-based keys or environment variables
- Easy integration with existing workflows and CI/CD pipelines

## Installation

Install PyTOMLEncrypt using pip:

```bash
pip install PyTOMLEncrypt
```

## Usage

### Generating a Key

```python
from PyTOMLEncrypt import generate_key, save_key

key = generate_key()
save_key(key=key, filename='secret.key')
```

### Encrypting a TOML File

```python
from PyTOMLEncrypt import encrypt_toml

encrypt_toml(input_file='config.toml', output_file='config.encrypted.toml', key_file='secret.key')
```

### Decrypting a TOML File

```python
from PyTOMLEncrypt import decrypt_toml

decrypt_toml(input_file='config.encrypted.toml', 'config.decrypted.toml', key_file='secret.key')
```

### Using Environment Variables

You can also use an environment variable to store the encryption key:

```python
import os
from PyTOMLEncrypt import encrypt_toml, decrypt_toml
# You can use setx <key_name> <key_value> via command prompt or subprocess.call to make the environment variable persistent.
# Ensure you restart your command prompt before using a newly set key, Python should be fine.
os.environ['PYTOML_ENCRYPT_KEY'] = 'your-secret-key'

encrypt_toml(input_file='config.toml', output_file='config.encrypted.toml', key_env_var='PYTOML_ENCRYPT_KEY')
decrypt_toml(input_file='config.encrypted.toml', output_file='config.decrypted.toml', key_env_var='PYTOML_ENCRYPT_KEY')
```

## Best Practices

1. Never commit your encryption key to version control.
2. Use different keys for different environments (development, staging, production).
3. Rotate your keys periodically for enhanced security.
4. When using in containers, inject the encryption key as an environment variable at runtime.

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
```
