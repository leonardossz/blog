# Publishing

Build public folder

    hugo -b https://amterano.net/

Copy to S3 folder

    aws s3 cp public/ s3://amterano.net/ --recursive

