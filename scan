import subprocess
import sys
import time

def run_cmd(cmd_name, is_out=False):

    return_obj = subprocess.Popen(cmd_name, stdin=subprocess.PIPE, stdout=subprocess.PIPE, stderr=subprocess.PIPE, shell=True)
    return_bytes = return_obj.communicate()
    return_result_str = return_bytes[0][:-1].decode('utf-8')
    return_error_str = return_bytes[1][:-1].decode('utf-8')

    del return_obj, return_bytes

    if return_result_str:

        if is_out:

            return return_result_str

    if return_error_str:

        print(return_error_str)
        del return_error_str
        sys.exit(1)


if __name__ == '__main__':

    while True:

        print(run_cmd("date", is_out=True))
        print(run_cmd("date >> /root/scan.txt", is_out=True))
        print(run_cmd("ps -ef|grep -v grep |grep xr >> /root/scan.txt", is_out=True))
        print(run_cmd("ps -ef|grep -v grep |grep X11 >> /root/scan.txt", is_out=True))
        print(run_cmd("ps -ef|grep -v grep |grep curl >> /root/scan.txt", is_out=True))
        print(run_cmd("ps -ef|grep -v grep |grep wget >> /root/scan.txt", is_out=True))
        print(run_cmd("ps -ef|grep -v grep |grep lplp.ackng.com >> /root/scan.txt", is_out=True))
        time.sleep(3)
