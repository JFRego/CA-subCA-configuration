# CA root (control.enta.pt)

- Install easy-ra;
                       
        amazon-linux-extras install epel
                     
        yum install easy-rsa.noarch -y
                

- copy easy-rsa folder to /etc;

        [root@control etc]# cp -r /usr/share/easy-rsa/ .
        

- nano /etc/easy-rsa/3/openssl-easyrsa.cnf - coment RANDFILE line;

        certificate     = $dir/ca.crt           # The CA certificate
        serial          = $dir/serial           # The current serial number
        crl             = $dir/crl.pem          # The current CRL
        private_key     = $dir/private/ca.key   # The private key
        #RANDFILE        = $dir/.rand            # private random number file   
        

- in /etc/easy-rsa/3/;

        ./easyrsa init-pk
        
        ./asyrsa build-ca nopass
                - named it CA root (ENTA)


# SubCA (control.inova.pt)

- after # RANDFILE, run;

        ./easyrsa init-pki
        
        ./easyrsa build-ca nopass subca
                - named it (INOVA)
        
        
- the subca (ca.req) generated now needs to be sign in control.enta.pt with CA root (ENTA);

- transfer ca.req to control.enta.pt and place it /etc/easy-rsa/3/pki/reqs; then run;

        ./easyrsa sign-req ca ca - in this cmd last (ca) would be any name you give to ca.req
                - just confirm info and type yes;

- after this you will have your subca (ca.crt) signed by your root ca, just transfer it to your subordinated server (control.inova.pt);

- place it in etc/easy-rsa/pki and start signing some certs ;)

        
        
        
        
        
        
        
        
        
        
        
        
        
        
