# Docker S3 cron backup container

This image provides a cron daemon that runs daily backups of directory /web/ and /tmp/backups/

It is recommended to connect /web/ directory to VOLUME with READ-ONLY files (i.e. /var/www/ folder of wordpress container for example) and to connect /tmp/backups/ directory to VOLUME with temp storage (i.e. /tmp/ of another container, for example mysqdump container) , the /tmp/backups/ directory's content will be deleted after the backup to S3

Originally forked from AckeeCZ/mariadb

Following ENV variables HAVE TO be specified:
 - `S3_ACCESS_KEY` S3 access key obtained from AWS
 - `S3_SECRET_KEY` S3 secret key obtained from AWS
 - `S3_URL` S3 url as a remote backup destionation. For S3://foo/bar/, enter only -e S3_URL=foo/bar
 
Following ENV variables CAN be specified:
 - `CRON_SCHEDULE` cron schedule string, default '0 2 * * *'

# How to run the container on Bluemix?

`cf ic run -e S3_ACCESS_KEY=youraccesskey -e S3_SECRET_KEY=yoursecretkey S3_URL=foo/bar -v wp-volume:/web -v backups:/tmp/backups/ -e CRON_SCHEDULE='0 1 * * *' registry.eu-gb.bluemix.net/organization/imagename`
