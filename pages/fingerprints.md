# CCR's public key fingerprints

These are CCR's ssh public key fingerprints for login nodes:

- `SHA256:QWv17p5d8CnZS7GPummIuLJW7vblXCWvMHlK7jrKtVA` (RSA)
- `SHA256:6PDsSxEFoBaiPvOWyX8N281imkGaQV81ypJXtSOVX/k` (ECDSA)
- `SHA256:QWv17p5d8CnZS7GPummIuLJW7vblXCWvMHlK7jrKtVA` (Ed25519)

To avoid having to manually verify ssh keys for every CCR server you login to,
you can add our ssh certificate to your `~.ssh/known_hosts`:  

```
@cert-authority *.ccr.buffalo.edu ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAACAQCjpY9sffG1O2xqrtRr+FZN73UNTrLtMO6uNMhymX4heJu8SLuMT69a4lkwLxuYfDm0IeM0JiOjCuiSWKIr34Iqj7wo3ksn46Mfa/B8V7EuOXu5HJ/w4pPefLvxH+gZBF1FRTQHfe5LVZh1ue2RPBose5rl0Y0/H6oLEfJW3O/1Vd2opPP7uFR416Ba94r2f5dJCUyPS+21lDti1fwVoz6yEGZzJ8WfoawDTRGGoRvO2lYOomq0tF2GkHhRDwe+UszlsYzhj+TpWG1cPKiygEJ0ey+cwjidkZPVfvDgtHGm9Q0CXc4mPcGiJhyl4MYtp4N4FhYLkTeDIb8t1F8lmhEDlu5cV0cB+B1cPgjVP4z9m1CYe+2TgkzCI3JStGlI9SCCXuSry4xZn3CZAB8dyQ/Iffw4BaZMisH+RALATvHoBfGS47t+SYbPKuB5663nhJrA7aj0wEA2FiYLheLiHr3picU9NBpX9cQ8OKD4KxMxghKbxxoErWA31tqDUsqQngOl8VN5XqhudqCmUToAlg/7W6cfZH/MK4h5SW17xEMkVQ11TId8pBf1gWmMAjSDTDLRGNx3LCK8snDmJvEkpxD/ADBuicve1HIZ2le/9655eD6IioM59MB30be6aLG6COSv4kBu5q3cohEFetAXiahnxyzuuKE1gIgff4osepbwUQ==  
```
