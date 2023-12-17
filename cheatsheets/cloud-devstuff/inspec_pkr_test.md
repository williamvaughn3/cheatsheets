

# InSpec and Packer

Provisioning with Packer and InSpec is a great way to ensure that your images are built with the correct configuration. 
InSpec can be used to test the configuration of the image before and after the provisioning steps are run.  
This allows you to test the configuration of the image at each step of the provisioning process.

```bash
provisioner "shell-local" {
    inline = [<<-INSPEC
        inspec exec ${local.inspecs}/dm \
            --key-files=${local.out_dir}/${build.ID}.key \
            --target ssh://${build.User}@${build.Host}:${build.Port} \
            --user=${build.User} \
            --sudo \
            --reporter html:${local.out_dir}/${build.ID}.after.html \
            junit:${local.out_dir}/${build.ID}.after.junit.xml
    INSPEC]
}

```

![Alt text](imgs/image12312411.png?raw=true "Packer InSpec build")